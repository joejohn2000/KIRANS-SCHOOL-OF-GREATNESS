# ANSWER SHEET — DEBUG & SOLVE HARD ASSESSMENT
**Date:** March 24, 2026
**Topics:** Days 7–10 — Sorting, Binary Search, Hash Tables, Linked Lists
**Total Marks:** 100

---

## SECTION A: SORTING (25 marks)

---

### Q1. The Merge Sort That Loses Data — (10 marks)

**Current output:** `mergeSort([5, 2, 8, 1, 9, 3])` returns `[5]`
**Expected output:** `[1, 2, 3, 5, 8, 9]`

#### (a) Both bugs

**Bug 1 — `arr.slice(mid + 1)` (line 6):**
```javascript
const right = mergeSort(arr.slice(mid + 1));  // WRONG
```
Should be `arr.slice(mid)`. Using `mid + 1` skips the element at index `mid` on every recursive split, silently dropping it.

**Bug 2 — right remainder never appended in `merge`:**
```javascript
while (i < left.length) { result.push(left[i]); i++; }
// right remainder loop is entirely missing
```
After the main `while` loop exits, any remaining elements in `right` are never added to `result`.

#### (b) Behaviour each bug causes

**Bug 1:** On each split, one element (at index `mid`) is permanently dropped. For `[5, 2, 8, 1, 9, 3]` (length 6, `mid=3`), `arr.slice(4)` = `[9, 3]` instead of the correct `arr.slice(3)` = `[1, 9, 3]`. Element `1` is lost before any merging occurs.

**Bug 2:** Whenever `left` is exhausted before `right` inside `merge`, the remaining tail of `right` is silently discarded. Combined with Bug 1, the two bugs interact: Bug 1 produces a length-1 right sub-array in many cases which then gets dropped by Bug 2, collapsing the entire sort down to the leftmost element of each top-level split.

Individually:
- Bug 1 only: `mergeSort([5, 2, 8, 1, 9, 3])` → `[5, 8, 9]` (element at each `mid` dropped, right remainders preserved)
- Bug 2 only: `mergeSort([5, 2, 8, 1, 9, 3])` → `[1, 2, 5]` (first halves kept, second halves of each merge lost)
- Both bugs together: → `[5]`

#### (c) Corrected implementation

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;

  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));      // Fix 1: mid, not mid + 1

  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let i = 0, j = 0;

  while (i < left.length && j < right.length) {
    if (left[i] <= right[j]) {
      result.push(left[i++]);
    } else {
      result.push(right[j++]);
    }
  }

  while (i < left.length) result.push(left[i++]);
  while (j < right.length) result.push(right[j++]);  // Fix 2: append right remainder

  return result;
}
```

**Time complexity:** O(n log n) — log n levels of recursion, O(n) merge work per level.
**Space complexity:** O(n) auxiliary — the merge step allocates new arrays totalling n elements per level.

---

### Q2. The Quick Sort That Hangs — (8 marks)

#### (a) The bug

```javascript
quickSort(arr, low, pivotIdx);    // WRONG — should be pivotIdx - 1
```

After `partition` returns `pivotIdx`, the pivot is in its correct final position and must not be included in either recursive sub-call. The left call should sort indices `low` to `pivotIdx - 1`. Using `pivotIdx` re-includes the pivot in the left sub-problem.

#### (b) Which class of inputs triggers infinite recursion and why

Infinite recursion occurs whenever `partition` returns `pivotIdx === high` for a given sub-call. In that case, the buggy left recursive call becomes `quickSort(arr, low, high)` — identical to the parent call — causing unbounded recursion.

`pivotIdx === high` happens when the pivot is the maximum element of the current sub-array, meaning all other elements are ≤ pivot and end up to its left, leaving the pivot at `high`. This occurs:

- **Always on sorted ascending arrays:** e.g., `[1, 2, 3]`. `partition([1,2,3], 0, 2)` has pivot = `arr[2]` = 3. All elements ≤ 3, so `i` advances to 1, then `arr[2]` swaps with itself. Returns `pivotIdx = 2 = high`. Infinite recursion on first call.
- **At sub-calls during any sort:** e.g., `[5, 2, 8, 1, 9, 3]`. The first `partition` returns `pivotIdx = 2`. The right sub-call `quickSort(arr, 3, 5)` sorts `[5, 9, 8]`. Here pivot = `arr[5]` = 8. Elements ≤ 8: 5, 8. `i` reaches 1. `arr[2]` swaps with `arr[5]`. Returns `pivotIdx = 2 = high` (relative to that sub-call where `high=2` in the sub-array). Infinite recursion in that sub-call.

In practice, **any input of length ≥ 2 will eventually trigger this**, because at some recursive level, the pivot will land at the `high` boundary of a sub-problem.

#### (c) Corrected line

```javascript
quickSort(arr, low, pivotIdx - 1);   // Fix: exclude pivot from left sub-problem
```

---

### Q3. Complexity Analysis Under Pressure — (7 marks)

#### (a) Time complexity of the given solution

**O(n + m log m)** where `n` = `nums.length` and `m` = number of distinct elements in `nums`.

- Building `freq`: one pass over `nums` → O(n).
- `Object.keys(freq)`: extracts `m` keys → O(m).
- `.sort(...)`: sorts `m` keys → O(m log m).
- `.slice(0, k)`: O(k).
- `.map(Number)`: O(k).

Since m ≤ n, worst case (all elements distinct) is **O(n log n)**.

#### (b) O(n) bucket sort approach

1. Build the frequency map in O(n): same as the current solution.
2. Create a `buckets` array of length `n + 1`. `buckets[f]` holds all numbers that appear exactly `f` times. The maximum possible frequency is `n` (all elements the same), so the array is sized `n + 1`. Building this takes O(m) ≤ O(n).
3. Iterate `buckets` from index `n` down to `1` (highest frequency first), collecting elements into the result until `k` elements are gathered. This scan is O(n).

Total: O(n). No sorting step required.

#### (c) The `Object.keys` integer-ordering bug

**The condition:** When all elements in `nums` are positive integers (or can be coerced to positive integer-like strings), `Object.keys()` returns them in **ascending numeric order** rather than insertion order. This is a V8/ECMAScript spec behaviour: integer-indexed string keys (non-negative integers that fit in a 32-bit unsigned int) are enumerated in ascending numeric order before other string keys.

**Why it causes wrong output:** Consider `nums = [1, 1, 2, 2, 2, 3]`, `k = 1`. The frequency map is `{1: 2, 2: 3, 3: 1}`. `Object.keys()` returns `['1', '2', '3']` in ascending numeric order (not insertion order). The `.sort((a, b) => freq[b] - freq[a])` comparator then sorts correctly by frequency desc → `['2', '1', '3']`. This works here. But with a tie: `nums = [3, 3, 1, 1]`, `k = 1`. `freq = {3: 2, 1: 2}`. `Object.keys()` = `['1', '3']` (numeric order). Sort puts them tied. Result depends on sort stability. In Node ≥ v11 (V8 7.0+), `Array.prototype.sort` is stable, so `['1', '3']` remains as-is → result is `[1]`. But the first-inserted key was `3`, so the "natural" expected answer might be `[3]`. This non-determinism in tie-breaking is the silent failure.

More critically: for mixed positive integers and non-integer keys (e.g., after inserting both `'2'` and `'-1'` as keys), `Object.keys()` returns positive-integer-like keys first, then the rest — silently reordering keys before `.sort()` even runs.

**Fix:** Use a `Map` instead of a plain object, which always preserves insertion order regardless of key type:

```javascript
function topKFrequent(nums, k) {
  const freq = new Map();
  for (const n of nums) {
    freq.set(n, (freq.get(n) || 0) + 1);
  }
  return [...freq.entries()]
    .sort((a, b) => b[1] - a[1])
    .slice(0, k)
    .map(([num]) => num);
}
```

---

## SECTION B: BINARY SEARCH (25 marks)

---

### Q4. Binary Search First Occurrence — Off-by-One — (9 marks)

**Current output:** `firstOccurrence([1, 2, 2, 2, 3], 2)` returns `3` (index of last occurrence)
**Expected output:** `1` (index of first occurrence — array is `[1, 2, 2, 2, 3]`, first `2` is at index 1)

#### (a) The bug

```javascript
low = mid + 1;   // WRONG — directs search rightward when a match is found
```

When `arr[mid] === target`, the code records `result = mid` (correct) but then sets `low = mid + 1`, which narrows the search to the right half — exactly the wrong direction for finding the *first* occurrence.

#### (b) Why it finds some occurrence but not the first

Each time a match is found, the candidate result is updated and the search continues — but rightward. Subsequent matches at higher indices overwrite `result`. When the loop terminates, `result` holds the rightmost index where `arr[mid] === target` was observed, which is the last occurrence, not the first.

#### (c) Corrected line

```javascript
if (arr[mid] === target) {
  result = mid;
  high = mid - 1;   // Fix: search LEFT half to find an earlier occurrence
}
```

---

### Q5. The Rotated Array Search That Cuts the Wrong Half — (9 marks)

#### (a) Trace for `search([6, 7, 0, 1, 2, 3, 4], target=6)`

```
Initial: low=0, high=6, nums=[6,7,0,1,2,3,4]

Iteration 1:
  mid = 3, nums[3] = 1
  nums[low]=nums[0]=6 > nums[mid]=1 → right half [1,2,3,4] is sorted
  Bug check: target=6 > nums[mid]=1 && target=6 <= nums[low]=6? → 6>1 ✓ AND 6<=6 ✓ → YES
  → low = mid + 1 = 4
  (target 6 is at index 0, LEFT side. We just eliminated the left half. It's gone.)

Iteration 2:
  low=4, high=6, mid=5, nums[5]=3
  nums[low]=nums[4]=2 <= nums[mid]=3 → left half [2,3] is sorted
  target=6: 6>=2 && 6<3? → NO → low = mid+1 = 6

Iteration 3:
  low=6, high=6, mid=6, nums[6]=4
  nums[6] !== 6
  nums[low]=nums[6]=4 <= nums[mid]=4 → left sorted (single element)
  target=6: 6>=4 && 6<4? → NO → low = 7

low(7) > high(6). Loop exits. Return -1.  ← WRONG (expected 0)
```

#### (b) The bug

```javascript
if (target > nums[mid] && target <= nums[low]) {   // Bug: nums[low] should be nums[high]
```

When the right half `[mid+1 .. high]` is sorted, the correct check is whether `target` falls within `[nums[mid+1], nums[high]]`, i.e., `target > nums[mid] && target <= nums[high]`. Using `nums[low]` instead of `nums[high]` checks against the wrong boundary. In the trace above, `nums[low] = 6` (the rotation point element) happens to equal the target, so the condition fires and incorrectly directs the search right, discarding the left half where target actually lives.

#### (c) Corrected implementation

```javascript
function search(nums, target) {
  let low = 0, high = nums.length - 1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);

    if (nums[mid] === target) return mid;

    if (nums[low] <= nums[mid]) {
      // Left half is sorted
      if (target >= nums[low] && target < nums[mid]) {
        high = mid - 1;
      } else {
        low = mid + 1;
      }
    } else {
      // Right half is sorted
      if (target > nums[mid] && target <= nums[high]) {   // Fix: nums[high], not nums[low]
        low = mid + 1;
      } else {
        high = mid - 1;
      }
    }
  }

  return -1;
}
```

**Time complexity:** O(log n) — each iteration eliminates half the remaining search space.

---

### Q6. Binary Search on Answer — Koko Eating Bananas — (7 marks)

#### (a) The bug

```javascript
if (canFinish(piles, mid, h)) {
  high = mid - 1;   // WRONG
}
```

When `canFinish` returns `true`, speed `mid` is a valid answer — but it may not be the *minimum* valid speed. We need to keep searching left to find a smaller valid speed. Setting `high = mid - 1` excludes `mid` from the remaining search space. If `mid` *is* the minimum, it gets discarded and the algorithm returns a lower value that fails `canFinish`.

**Verification:** `minEatingSpeed([4, 9, 4], 9)` should return `2`.
- `canFinish(1)`: ceil(4/1)+ceil(9/1)+ceil(4/1) = 17 > 9 → false.
- `canFinish(2)`: ceil(4/2)+ceil(9/2)+ceil(4/2) = 2+5+2 = 9 ≤ 9 → true. Answer = 2.

Buggy trace: `low=1, high=9`.
- `mid=5`. `canFinish(5)` = 1+2+1=4 ≤ 9 → true. `high = 4`.
- `low=1, high=4`. `mid=2`. `canFinish(2)` = 2+5+2=9 ≤ 9 → true. `high = 1`.
- `low=1, high=1`. `low < high`? NO. Returns `low = 1`. **Wrong** (expected 2).

#### (b) Corrected line

```javascript
if (canFinish(piles, mid, h)) {
  high = mid;       // Fix: keep mid as a candidate, continue searching left
}
```

#### (c) Invariant and time complexity

**Invariant:** At all times, the true minimum eating speed lies within `[low, high]` inclusive. The loop condition `while (low < high)` terminates when `low === high`, at which point both pointers have converged to the single remaining candidate — the minimum valid speed.

`high = mid - 1` breaks this invariant by potentially dropping the answer from the search space. `high = mid` preserves it: if `mid` is valid, it remains the upper bound while we search for something smaller; if nothing smaller is valid, `low` converges to `mid`.

**Time complexity:** O(n log m)
- `m` = `Math.max(...piles)` — size of the speed search space.
- Binary search runs O(log m) iterations.
- Each `canFinish` call is O(n) — one pass over all piles.

**Space complexity:** O(1).

---

## SECTION C: HASH TABLES — DEEP DIVE (25 marks)

---

### Q7. The Broken Hash Table — (12 marks)

#### (a) All three bugs

| # | Location | Bug |
|---|---|---|
| 1 | `set`, `bucket.append(key, value)` | `list.append()` takes exactly one argument; passing two raises `TypeError` |
| 2 | `_hash`, `sum(ord(c) for c in key)` | `ord(c)` requires a string character; any non-string key raises `TypeError: 'int' object is not iterable` |
| 3 | `resize`, no guard on `new_size` | Calling `resize(0)` sets `self.size = 0`, causing `ZeroDivisionError` in `_hash` (`% 0`) |

#### (b) Runtime behaviour of each bug

**Bug 1:** Every `set()` call that inserts a *new* key crashes immediately:
```
TypeError: list.append() takes exactly one argument (2 given)
```
The update path (`bucket[i] = (key, value)`) is correct and unaffected, so `set` only works for keys already in the bucket.

**Bug 2:** Any call with a non-string key — e.g., `ht.set(42, 'answer')` — raises:
```
TypeError: 'int' object is not iterable
```
because `for c in key` tries to iterate an integer.

**Bug 3:** `resize(0)` sets `self.size = 0` then calls `self.set(k, v)` which calls `self._hash(k)` which computes `... % 0`:
```
ZeroDivisionError: integer modulo by zero
```
Resizing to a value smaller than the current item count also silently degrades performance (more collisions, longer chains), though it does not crash.

#### (c) Corrected class

```python
class HashTable:
    def __init__(self, size=10):
        self.size = size
        self.table = [[] for _ in range(size)]

    def _hash(self, key):
        return hash(key) % self.size          # Fix 2: use built-in hash() for any hashable type

    def set(self, key, value):
        index = self._hash(key)
        bucket = self.table[index]

        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket[i] = (key, value)
                return

        bucket.append((key, value))           # Fix 1: append a tuple, not two separate args

    def get(self, key):
        index = self._hash(key)
        bucket = self.table[index]
        for k, v in bucket:
            if k == key:
                return v
        return None

    def delete(self, key):
        index = self._hash(key)
        bucket = self.table[index]
        for i, (k, v) in enumerate(bucket):
            if k == key:
                del bucket[i]
                return

    def load_factor(self):
        total_items = sum(len(b) for b in self.table)
        return total_items / self.size

    def resize(self, new_size):
        if new_size <= 0:                     # Fix 3: guard against invalid size
            raise ValueError("new_size must be > 0")
        old_table = self.table
        self.size = new_size
        self.table = [[] for _ in range(new_size)]
        for bucket in old_table:
            for k, v in bucket:
                self.set(k, v)
```

---

### Q8. LRU Cache — The Update That Forgets Its Place — (8 marks)

#### (a) Trace for `capacity=2`, ops: `put(1,1)`, `put(2,2)`, `put(1,10)`, `put(3,3)`, `get(1)`

JavaScript `Map` maintains insertion order. LRU = first key in map (`map.keys().next()`), MRU = last key.

```
put(1, 1):  key 1 not in map. size(0) < 2. Insert. map = {1:1}

put(2, 2):  key 2 not in map. size(1) < 2. Insert. map = {1:1, 2:2}
            LRU=1, MRU=2.

put(1, 10): key 1 IS in map. Bug: map.set(1, 10) — value updated but key stays at its
            ORIGINAL position (front of map). map = {1:10, 2:2}
            Key 1 is still the LRU. It should be MRU (just accessed/updated).

put(3, 3):  key 3 not in map. size(2) >= 2. Evict LRU = key 1. map.delete(1).
            map = {2:2}. Insert 3. map = {2:2, 3:3}.
            Key 1 (value 10) has been evicted — but it was just updated! It should have been MRU.

get(1):     map.has(1) → false. Returns -1.
            Expected: 10 (key 1 was updated to 10 and should still be in cache as MRU).
```

**Result:** `get(1)` returns `-1`. Expected: `10`. The update in `put(1, 10)` failed to promote key 1 to MRU, so it was wrongly evicted.

#### (b) Why `map.set(key, value)` alone is insufficient

`Map.prototype.set()` updates the *value* for an existing key but does not change the key's position in insertion order. The LRU eviction logic relies entirely on insertion order: the oldest-inserted key (the first in the map) is always the LRU candidate. To mark a key as "most recently used", it must be deleted and re-inserted, moving it to the end of the map's internal ordering. Calling `map.set` on an existing key skips this re-ordering step.

#### (c) Corrected `put` method

```javascript
put(key, value) {
  if (this.map.has(key)) {
    this.map.delete(key);      // Remove from current position
    this.map.set(key, value);  // Re-insert at end (MRU position)
    return;
  }
  if (this.map.size >= this.capacity) {
    const lruKey = this.map.keys().next().value;
    this.map.delete(lruKey);
  }
  this.map.set(key, value);
}
```

---

### Q9. Longest Consecutive Sequence — Complexity Claim — (5 marks)

#### (a) Is the candidate correct?

**No.** The O(n²) claim is wrong.

#### (b) Actual complexity — rigorous proof

**Time complexity: O(n)**

The `if (!numSet.has(num - 1))` guard is the key. The inner `while` loop only runs when `num` is the *start* of a consecutive sequence — meaning `num - 1` is not in the set. Every element belongs to exactly one consecutive sequence and is therefore the start of exactly one sequence.

**Formal bound:** Each element `x` in `numSet` can be visited by the `while` loop at most once — when processing the start of `x`'s sequence. Once `x` has been counted (`current` passes through `x`), no other outer `for` iteration will trigger the `while` to visit `x` again (because only sequence-start elements enter the `while` block). The total number of `while` iterations across *all* outer iterations is therefore bounded by `|numSet|` ≤ n.

Combined with the O(n) outer `for` loop (iterates over each unique element once), the total work is O(n) + O(n) = **O(n)**.

This is an amortised argument: the inner loop is "expensive" for the start of a long sequence, but that cost is spread across all elements of the sequence. No element is visited twice by the inner loop across the entire execution.

**Space complexity: O(n)** — the `Set` stores at most `n` distinct values.

---

## SECTION D: LINKED LISTS (25 marks)

---

### Q10. The Linked List Reversal That Corrupts the List — (10 marks)

#### (a) Trace for `1 → 2 → 3 → 4 → 5`

**Before loop starts:**
- `prev = null`, `curr = node(1)`, list intact: `1→2→3→4→5`

**Iteration 1:**
```
curr.next = prev           →  node(1).next = null
                              *** node(2) through node(5) are now unreachable — reference lost ***
prev = curr                →  prev = node(1)
curr = curr.next           →  curr = null   (because node(1).next was just set to null)
```
After iteration 1: `prev = node(1)`, `curr = null`. Loop exits.

The loop terminates after a single iteration. All nodes except `node(1)` are lost permanently. The function returns `node(1)` — a single-node list `[1]`.

There is no "second iteration" because `curr` became `null` in iteration 1.

#### (b) The bug

```javascript
curr.next = prev;   // Overwrites the only pointer to the rest of the list
// ...
curr = curr.next;   // curr.next is now prev (null), not the original next node
```

`curr.next` is overwritten before its original value is saved. The reference to the remainder of the list is permanently destroyed before it can be used to advance `curr`.

#### (c) Corrected function

```javascript
function reverseList(head) {
  let prev = null;
  let curr = head;

  while (curr !== null) {
    const nextNode = curr.next;   // Fix: save next BEFORE overwriting
    curr.next = prev;
    prev = curr;
    curr = nextNode;              // Advance using the saved reference
  }

  return prev;
}
```

**Full trace on `1→2→3→4→5`:**
```
Start: prev=null, curr=1
Iter 1: next=2,    1.next=null, prev=1, curr=2
Iter 2: next=3,    2.next=1,    prev=2, curr=3
Iter 3: next=4,    3.next=2,    prev=3, curr=4
Iter 4: next=5,    4.next=3,    prev=4, curr=5
Iter 5: next=null, 5.next=4,    prev=5, curr=null
Return: 5 → 4 → 3 → 2 → 1  ✓
```

---

### Q11. Floyd's Cycle Detection — Wrong Start — (8 marks)

#### (a) The bug and which input causes a crash

```javascript
let fast = head.next;   // Bug
```

**Input that causes a crash: `head = null` (empty list).**

`head.next` dereferences `null`, immediately throwing:
```
TypeError: Cannot read properties of null (reading 'next')
```

This crash happens before the loop body executes, regardless of whether a cycle exists.

A secondary correctness issue exists on a **single-node list with no cycle** (`head = node(1)`, `node(1).next = null`):
- `slow = node(1)`, `fast = null`.
- Loop condition: `slow !== fast` → `node(1) !== null` → `true`.
- Inside: `fast === null` → return `false`. Correct result, but reached via fragile path.

And on a **single-node self-loop** (`node(1).next = node(1)`):
- `slow = node(1)`, `fast = node(1).next = node(1)`.
- Loop condition: `slow !== fast` → `node(1) !== node(1)` → `false`. Loop never runs. Returns `true`. Correct, but again by coincidence.

#### (b) Why the original (first version) is correct and this version is not

**Original version:**
```javascript
let slow = head;
let fast = head;
while (fast !== null && fast.next !== null) { ... }
```

- Both start at `head`. If `head = null`, the `while` condition short-circuits immediately — no dereference, no crash.
- Each iteration: `slow` moves 1 step, `fast` moves 2 steps. If no cycle, `fast` reaches `null` safely. If a cycle exists, `fast` laps `slow` — they are guaranteed to meet within the cycle length iterations.
- The meeting check `if (slow === fast) return true` is placed *after* advancing, avoiding the false positive of both starting at the same node (which would trigger `slow === fast` immediately before any movement).

**This (buggy) version:**
- `fast = head.next` crashes on `null` input.
- The termination structure (`while (slow !== fast)`) starts with `slow !== fast` potentially `true` even for no-cycle lists, but the `null` guard inside the loop (`if (fast === null ... return false`) rescues some cases — making it brittle and harder to reason about.

#### (c) Floyd's guarantee, time and space complexity

**Guarantee:** If a cycle exists, `slow` and `fast` will meet at some node within the cycle within O(n) steps. If no cycle exists, `fast` reaches `null` within O(n) steps.

**Time complexity: O(n)** — in the worst case, both pointers traverse the list a bounded number of times proportional to n.

**Space complexity: O(1)** — only two pointer variables, regardless of list length. This is the primary advantage over a `Set`-based approach, which requires O(n) space to track visited nodes.

---

### Q12. Merge Two Sorted Lists — The Dummy Node Trap — (7 marks)

#### (a) The bug

```javascript
return dummy;   // WRONG — returns the sentinel node, not the merged list head
```

`dummy` is a placeholder node with value `0` that was never part of either input list. Returning it prepends a spurious `0` to the result.

**Evidence:** For inputs `[1,3,5]` and `[2,4,6]`, the buggy function returns `[0,1,2,3,4,5,6]` instead of `[1,2,3,4,5,6]`.

#### (b) What `dummy` represents and what to return

`dummy` is a sentinel head node — an empty placeholder that allows the merge loop to write `curr.next = ...` uniformly from the first iteration onward, without needing to special-case initialising the result head. It is an implementation detail, not a real element.

The actual merged list begins at `dummy.next` (the first node that was spliced in during the loop).

#### (c) Corrected return statement and dummy node explanation

```javascript
return dummy.next;   // Fix: skip the sentinel, return first real merged node
```

**Why the dummy node pattern is useful:**

Without it, you must handle the first node specially:
```javascript
// Without dummy — awkward
let head = null, curr = null;
if (!l1 || (l2 && l2.val < l1.val)) { head = l2; curr = l2; l2 = l2.next; }
else                                 { head = l1; curr = l1; l1 = l1.next; }
while (l1 && l2) { ... }
```

With a dummy node, the first-node case is identical to all subsequent cases — `curr.next = ...` always has a valid `curr`. The sentinel is discarded at the end via `dummy.next`. This pattern applies broadly: any linked list problem that builds a new list from scratch (merge k lists, partition list, remove nth from end) benefits from this approach.

---

## MARK SUMMARY

| Q | Topic | Max | Key points |
|---|---|---|---|
| Q1 | Merge sort — two bugs | 10 | Bug 1: `slice(mid+1)` → `slice(mid)`. Bug 2: missing right remainder loop. Combined output: `[5]` |
| Q2 | Quick sort — infinite recursion | 8 | `pivotIdx` → `pivotIdx - 1`. Triggers whenever `partition` returns `pivotIdx === high` — affects nearly all inputs |
| Q3 | Top-K frequent — complexity | 7 | O(n + m log m); bucket sort O(n); `Object.keys` integer numeric ordering affects tie-breaking; fix: use `Map` |
| Q4 | Binary search first occurrence | 9 | `low = mid+1` → `high = mid-1` when match found. Buggy returns index 3 (last), correct returns 1 (first) |
| Q5 | Rotated array search | 9 | `nums[low]` → `nums[high]` in right-sorted branch. `search([6,7,0,1,2,3,4], 6)` returns -1, expected 0 |
| Q6 | Binary search on answer | 7 | `high = mid-1` → `high = mid`. `minEatingSpeed([4,9,4], 9)` returns 1 (wrong), should return 2 |
| Q7 | Hash table — 3 bugs | 12 | `append(k,v)` → `append((k,v))`; `ord(c)` → `hash(key)`; no `resize(0)` guard |
| Q8 | LRU cache | 8 | `map.set(key,value)` on existing key doesn't move to MRU; must `delete` then `re-insert` |
| Q9 | Consecutive sequence complexity | 5 | O(n), not O(n²). Each element visited by inner while at most once — amortised argument |
| Q10 | List reversal — pointer loss | 10 | Save `curr.next` before overwriting. All nodes lost after iteration 1; returns `[1]` |
| Q11 | Floyd's cycle — wrong start | 8 | `fast = head.next` crashes on `null`. Correct version starts both at `head`, guards with `fast !== null` |
| Q12 | Merge lists — wrong return | 7 | `return dummy` → `return dummy.next`. Buggy result starts with spurious `0` |
| **Total** | | **100** | |
