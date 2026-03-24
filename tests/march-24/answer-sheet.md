# ANSWER SHEET — DEBUG & SOLVE HARD ASSESSMENT
**Date:** March 24, 2026
**Topics:** Days 7–10 — Sorting, Binary Search, Hash Tables, Linked Lists
**Total Marks:** 100

---

## SECTION A: SORTING (25 marks)

---

### Q1. The Merge Sort That Loses Data — (10 marks)

**Current output:** `mergeSort([5, 2, 8, 1, 9, 3])` returns `[2, 5, 9]` (elements dropped)
**Expected output:** `[1, 2, 3, 5, 8, 9]`

#### (a) Both bugs

**Bug 1 — `arr.slice(mid + 1)` on line 6:**
```javascript
const right = mergeSort(arr.slice(mid + 1));  // WRONG
```
Should be `arr.slice(mid)`. Using `mid + 1` skips the element at index `mid`, silently dropping it from the sort entirely.

**Bug 2 — remainder of `right` is never appended after the merge loop:**
```javascript
// The while loop for left's remainder exists, but right's is missing
while (i < left.length) { result.push(left[i]); i++; }
// right remainder: MISSING
```
When the `while (i < left.length && j < right.length)` loop ends because `right` is exhausted first, the remaining elements of `left` are appended. But the inverse — remaining `right` elements — are never appended.

#### (b) Behaviour each bug causes

- **Bug 1:** Every recursive split loses the middle element. For `[5, 2, 8, 1, 9, 3]` (length 6, mid=3), `right = arr.slice(4)` = `[9, 3]` instead of `arr.slice(3)` = `[1, 9, 3]`. The element `1` disappears permanently.
- **Bug 2:** Whenever the left sub-array is exhausted first in `merge()`, any remaining tail of `right` is silently dropped. This causes the merge step to produce arrays shorter than their input.

#### (c) Corrected implementation

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;

  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));     // Fix 1: mid, not mid + 1

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
**Space complexity:** O(n) — merge creates a new array of total size n per level, but only one level exists at a time.

---

### Q2. The Quick Sort That Hangs — (8 marks)

#### (a) The bug

```javascript
quickSort(arr, low, pivotIdx);    // WRONG — should be pivotIdx - 1
```

After `partition` returns `pivotIdx`, the pivot is already in its correct final position. The left recursive call should sort `low` to `pivotIdx - 1`. Using `pivotIdx` includes the pivot itself in the sub-problem.

#### (b) Which input triggers infinite recursion and why

When the pivot ends up at `low` (i.e., `pivotIdx === low`), `partition` returns `low`. The call `quickSort(arr, low, low)` fires. Inside, `low < high` is false so it returns immediately — that's fine. But the faulty version calls `quickSort(arr, low, pivotIdx)` which is `quickSort(arr, low, low)` — also fine in that step.

The infinite loop is triggered on already-sorted or reverse-sorted arrays. Example: `[1, 2, 3]`.
- `partition([1,2,3], 0, 2)`: pivot = `arr[2]` = 3. No swaps occur. Returns `pivotIdx = 2`.
- Left call: `quickSort(arr, 0, 2)` — same call as the parent. **Infinite recursion.**

More precisely: whenever the pivot is chosen as the maximum element of the sub-array (pivotIdx = high), the faulty left call becomes `quickSort(arr, low, high)` — identical to the parent call.

#### (c) Corrected line

```javascript
quickSort(arr, low, pivotIdx - 1);   // Fix: exclude pivot from left sub-problem
```

---

### Q3. Complexity Analysis Under Pressure — (7 marks)

#### (a) Time complexity of the given solution

**O(n + m log m)** where `n` = length of `nums` and `m` = number of distinct elements.

- Building `freq`: O(n) — one pass over `nums`.
- `Object.keys(freq)`: O(m).
- `.sort(...)`: O(m log m) — sorting `m` distinct keys.
- `.slice(0, k)`: O(k).
- `.map(Number)`: O(k).

Dominant term: O(n + m log m). Since m ≤ n, this is O(n log n) in the worst case (all elements distinct).

#### (b) O(n) bucket sort approach

1. Build the frequency map in O(n): same as the current solution.
2. Create a `buckets` array of length `n + 1`, where `buckets[freq]` holds all numbers with that frequency (index = frequency, max possible frequency = n).
3. Iterate `buckets` from right to left (highest frequency first), collecting elements until `k` elements are gathered.

This runs in O(n): building freq is O(n), building buckets is O(n), scanning buckets is O(n).

#### (c) The negative number bug

```javascript
.map(Number)
```

`Object.keys()` always returns strings. When `nums` contains negative numbers, e.g., `-1`, the key is the string `"-1"`. `Number("-1")` correctly returns `-1` — so this is actually fine.

The actual silent bug is:

```javascript
return Object.keys(freq)
  .sort((a, b) => freq[b] - freq[a])
```

`Object.keys()` returns string keys. The comparator `freq[b] - freq[a]` works because property access with a string key still works. But: **`Object.keys()` does not guarantee insertion order for non-integer-like keys in all JS engines.** For integer-like string keys (e.g., `"1"`, `"2"`, `"100"`), V8 (Node.js) sorts them in ascending numeric order before returning them from `Object.keys()`, which means the frequency sort is applied to an already numerically-reordered key list. This can silently produce wrong results when element values are positive integers and frequency ties exist.

**Fix:** Use a `Map` instead of a plain object to preserve insertion order:

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

**Current output:** `firstOccurrence([1, 2, 2, 2, 3], 2)` returns `3` (last occurrence index)
**Expected output:** `2` (index of first occurrence)

#### (a) The bug

```javascript
low = mid + 1;   // WRONG — should search LEFT half, not right
```

When `arr[mid] === target`, the code records `result = mid` but then moves `low` to `mid + 1`, which searches the right half for more occurrences. This finds the *last* occurrence, not the first.

#### (b) Why it finds some occurrence but not the first

When a match is found, the algorithm correctly records it as a candidate. However, by moving `low = mid + 1`, it directs the search toward higher indices — the direction away from the first occurrence. It keeps overwriting `result` with later indices, leaving `result` holding the rightmost match when the loop ends.

#### (c) Corrected line

```javascript
if (arr[mid] === target) {
  result = mid;
  high = mid - 1;   // Fix: search LEFT half to find earlier occurrence
}
```

---

### Q5. Rotated Array Search — Missing Half — (9 marks)

#### (a) Trace for `search([4, 5, 6, 7, 0, 1, 2], target=0)`

```
Initial: low=0, high=6

Iteration 1:
  mid = 3, nums[3] = 7
  nums[low]=4 <= nums[mid]=7 → left half [4,5,6,7] is sorted
  target=0: is 0 >= 4 && 0 < 7? → NO
  → low = mid + 1 = 4

Iteration 2:
  low=4, high=6, mid=5, nums[5]=1
  nums[low]=nums[4]=0 <= nums[mid]=1 → left half [0,1] is sorted
  target=0: is 0 >= 0 && 0 < 1? → YES
  → high = mid - 1 = 4

Iteration 3:
  low=4, high=4, mid=4, nums[4]=0
  nums[4] === target → return 4 ✓
```

The given test case actually returns the correct answer. The bug manifests on a different input.

**Revealing test case:** `search([3, 1], target=1)`

```
low=0, high=1, mid=0, nums[0]=3
nums[low]=3 <= nums[mid]=3 → left sorted
target=1: is 1 >= 3 && 1 < 3? → NO
→ low = mid + 1 = 1

low=1, high=1, mid=1, nums[1]=1
nums[1] === target → return 1 ✓  (works here too)
```

**Actual bug case:** `search([5, 1, 3], target=3)`

```
low=0, high=2, mid=1, nums[1]=1
nums[low]=5 > nums[mid]=1 → right half is sorted
target=3: is 3 > nums[mid]=1 && 3 <= nums[high]=3? → YES
→ low = mid + 1 = 2

low=2, high=2, mid=2, nums[2]=3 → return 2 ✓
```

The true problematic case for the `high = mid - 1` bug:

`search([3, 5, 1], target=3)` with the buggy `else` branch:

```
low=0, high=2, mid=1, nums[1]=5
nums[low]=3 <= nums[mid]=5 → left sorted
target=3: is 3 >= 3 && 3 < 5? → YES → high = mid-1 = 0

low=0, high=0, mid=0, nums[0]=3 → return 0 ✓ (still works)
```

The logic is actually correct as written for the standard rotated search. The subtle error is in the comment `// Bug — wrong in one case`. The real issue: the `high = mid - 1` in the else of the right-sorted branch is correct. The actual bug is that when `nums[low] === nums[mid]` (duplicates), the condition `nums[low] <= nums[mid]` is true but the left half may not be genuinely sorted. **The code has no bug for the no-duplicates variant (LeetCode #33)** but fails for the duplicates variant (LeetCode #81).

#### (b) The bug (for duplicates variant)

When `nums[low] === nums[mid]`, we cannot determine which half is sorted. The fix for the duplicates variant:

```javascript
if (nums[low] === nums[mid]) {
  low++;  // shrink the window and retry
}
```

#### (c) Corrected implementation (handles duplicates)

```javascript
function search(nums, target) {
  let low = 0, high = nums.length - 1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);

    if (nums[mid] === target) return mid;

    // Handle duplicates
    if (nums[low] === nums[mid] && nums[mid] === nums[high]) {
      low++;
      high--;
    } else if (nums[low] <= nums[mid]) {
      // Left half is sorted
      if (target >= nums[low] && target < nums[mid]) {
        high = mid - 1;
      } else {
        low = mid + 1;
      }
    } else {
      // Right half is sorted
      if (target > nums[mid] && target <= nums[high]) {
        low = mid + 1;
      } else {
        high = mid - 1;
      }
    }
  }

  return -1;
}
```

**Time complexity:** O(log n) average, O(n) worst case when duplicates force linear shrinking.

---

### Q6. Binary Search on Answer — Koko Eating Bananas — (7 marks)

#### (a) The bug

```javascript
if (canFinish(piles, mid, h)) {
  high = mid - 1;   // WRONG
}
```

When `canFinish` returns `true` (speed `mid` is sufficient), we want to try a *lower* speed — but we must still consider `mid` itself as a valid answer. Setting `high = mid - 1` excludes `mid` from the search space. If `mid` is the minimum valid speed, it gets discarded, and the algorithm returns a value smaller than the true answer (which then fails `canFinish`).

#### (b) Corrected line

```javascript
if (canFinish(piles, mid, h)) {
  high = mid;       // Fix: keep mid as a candidate, search left including mid
}
```

#### (c) Invariant explanation and time complexity

**Invariant:** At all times, the answer lies in the range `[low, high]` inclusive. The loop terminates when `low === high`, at which point both pointers have converged on the minimum valid speed.

Using `high = mid - 1` breaks this invariant by potentially excluding the answer. Using `high = mid` preserves it: if `mid` is valid, we keep it as the upper bound and search for something smaller; if nothing smaller is valid, `low` will converge to `mid`.

The loop condition `while (low < high)` (not `<=`) ensures termination: when `low === high`, we stop and return `low`.

**Time complexity:** O(n log m) where:
- `m` = `Math.max(...piles)` — the search space for speed.
- Each `canFinish` call is O(n) — one pass over all piles.
- Binary search runs O(log m) iterations.

**Space complexity:** O(1) — no auxiliary data structures.

---

## SECTION C: HASH TABLES — DEEP DIVE (25 marks)

---

### Q7. The Broken Hash Table — (12 marks)

#### (a) All three bugs

**Bug 1 (critical) — `bucket.append(key, value)` line 16:**
```python
bucket.append(key, value)   # WRONG — append takes one argument
```
`list.append()` in Python accepts exactly one argument. This raises `TypeError: list.append() takes exactly one argument (2 given)`. The intent is to append a tuple.

**Bug 2 (subtle) — `load_factor` returns a float that doesn't account for a useful threshold:**
```python
return total_items / self.size   # technically computes load factor correctly
```
Wait — this is actually correct arithmetic. The true Bug 2 is that `load_factor` is never called during `set()`. A hash table should auto-resize when load factor exceeds a threshold (typically 0.7). Without this, the table degrades to O(n) lookups. However, since `resize` exists as a separate method, the missing call is the design flaw, not a code bug per se.

The actual Bug 2 is in `resize`:
```python
self.table = [[] for _ in range(new_size)]   # Bug 3 — re-hashing uses new size immediately
```
Wait — this is Bug 3. Let me re-identify:

**Bug 2 (subtle) — Integer keys are not supported:**
```python
def _hash(self, key):
    return sum(ord(c) for c in key) % self.size
```
`ord(c)` only works on strings. Passing an integer key raises `TypeError: 'int' object is not iterable`. A production hash table should handle any hashable key via `hash(key)`.

**Bug 3 (subtle) — `resize` updates `self.size` before re-hashing:**
```python
self.size = new_size
self.table = [[] for _ in range(new_size)]   # self.size already changed — this is fine
```
Actually the order is: set `self.size`, then create new table, then call `self.set(k, v)` which uses `self.size` for hashing. The hashing uses the new size — which is correct. Bug 3 is that if `resize` is called with `new_size < current number of items`, the load factor increases beyond 1 and performance degrades, but there is no guard. More critically: `resize` does not validate `new_size > 0`.

Corrected identification of the three bugs for this question:

| # | Location | Bug |
|---|---|---|
| 1 | `set`, line `bucket.append(key, value)` | `append` called with 2 args instead of a tuple — TypeError |
| 2 | `_hash` | `ord(c)` only works for string keys; any non-string key crashes |
| 3 | `resize` | No validation: `new_size` could be 0 (ZeroDivisionError in `_hash`) or smaller than item count |

#### (b) Runtime behaviour of each bug

- **Bug 1:** Every `set()` call on a new key crashes with `TypeError`. Existing keys can be updated (the update path uses `bucket[i] = ...` which is correct), but inserting any new key fails.
- **Bug 2:** Any call with a non-string key (e.g., `ht.set(1, 'a')`) raises `TypeError: 'int' object is not iterable`.
- **Bug 3:** `resize(0)` causes `ZeroDivisionError` in `_hash` (`% 0`). Resizing to fewer buckets than items creates high-collision chains, silently degrading O(1) to O(n).

#### (c) Corrected class

```python
class HashTable:
    def __init__(self, size=10):
        self.size = size
        self.table = [[] for _ in range(size)]

    def _hash(self, key):
        return hash(key) % self.size          # Fix 2: use built-in hash() for any key type

    def set(self, key, value):
        index = self._hash(key)
        bucket = self.table[index]

        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket[i] = (key, value)
                return

        bucket.append((key, value))           # Fix 1: append a tuple, not two args

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
        if new_size <= 0:                     # Fix 3: guard against invalid sizes
            raise ValueError("new_size must be > 0")
        old_table = self.table
        self.size = new_size
        self.table = [[] for _ in range(new_size)]
        for bucket in old_table:
            for k, v in bucket:
                self.set(k, v)
```

---

### Q8. LRU Cache — Wrong Eviction — (8 marks)

#### (a) Trace for `capacity=2`, ops: `put(1,1)`, `put(2,2)`, `get(1)`, `put(3,3)`, `get(2)`

JavaScript `Map` maintains insertion order. The LRU (least recently used) key is always `map.keys().next().value` (the first key inserted).

```
put(1, 1):  map not full → map = {1:1}
put(2, 2):  map not full → map = {1:1, 2:2}
get(1):     key 1 exists → delete 1, re-insert → map = {2:2, 1:1}   (1 is now MRU)
put(3, 3):  map.size (2) >= capacity (2)
              lruKey = map.keys().next().value = 2   ← evict key 2 (correct, 2 is LRU)
              map.delete(2) → map = {1:1}
              map.set(3, 3) → map = {1:1, 3:3}
get(2):     map.has(2) → false → returns -1
```

The trace shows the logic is actually correct here. The bug in `put` is more subtle: when a key already exists and is being updated, the code deletes it and re-inserts it *after* the eviction check. That means if the map is at capacity and the key being `put` already exists, the sequence is:

```javascript
if (this.map.has(key)) {
  this.map.delete(key);          // size drops to capacity - 1
}
if (this.map.size >= this.capacity) {  // false! size is now capacity - 1
  // eviction skipped even if a different key should be evicted
}
this.map.set(key, value);        // size back to capacity — but order is wrong
```

The real bug: when the same key is updated (already exists), deleting first and then checking size means the eviction block runs on `size = capacity - 1`, which is `< capacity`, so eviction is skipped — this is correct behaviour for an update. The code is actually not buggy in the described scenario.

The actual bug is: `map.set(key, value)` after the eviction block means the new key is inserted *after* we already evicted the LRU. This is fine. The described "inserting in wrong order" comment in the question points to the fact that when the key already exists, the re-insertion correctly moves it to MRU — this is right.

**Demonstrating the real bug:** `capacity=2`, `put(1,1)`, `put(2,2)`, `put(1,10)` (update key 1).

```
put(1, 1):  map = {1:1}
put(2, 2):  map = {1:1, 2:2}
put(1, 10): map.has(1) → delete 1 → map = {2:2}, size=1
            size(1) >= capacity(2)? NO → no eviction
            map.set(1, 10) → map = {2:2, 1:10}
```

Map order is `{2:2, 1:10}` — key 2 is LRU, key 1 is MRU. This is correct. The implementation is actually correct.

**The stated bug (wrong insertion order) manifests as:** when an existing key is updated, it correctly moves to MRU. The issue would only appear if `map.set` were called before `map.delete`, which it is not in this code. The `put` method is correct as written.

**Verdict:** The `put` bug as annotated in the question is a red herring — the implementation is correct. The real gotcha is recognising it is correct and being able to explain why, rather than blindly agreeing there is a bug.

#### (b) The actual LRU implementation (confirmed correct)

```javascript
put(key, value) {
  if (this.map.has(key)) {
    this.map.delete(key);
  } else if (this.map.size >= this.capacity) {
    // Only evict if this is a NEW key, not an update
    const lruKey = this.map.keys().next().value;
    this.map.delete(lruKey);
  }
  this.map.set(key, value);
}
```

The corrected version separates the `update` path from the `evict + insert` path using `if/else if`, preventing the size check from running incorrectly on updates.

#### (c) Corrected `put`

```javascript
put(key, value) {
  if (this.map.has(key)) {
    this.map.delete(key);
  } else if (this.map.size >= this.capacity) {
    const lruKey = this.map.keys().next().value;
    this.map.delete(lruKey);
  }
  this.map.set(key, value);
}
```

---

### Q9. Longest Consecutive Sequence — Complexity Claim — (5 marks)

#### (a) Is the candidate correct?

**No.** The candidate's O(n²) claim is wrong.

#### (b) Actual complexity — rigorous proof

**Time complexity: O(n)**

The key insight is in the `if (!numSet.has(num - 1))` guard. The `while` loop inside only executes for a number `num` that is the **start** of a consecutive sequence (i.e., `num - 1` is not in the set). Every number in the set belongs to exactly one consecutive sequence and is therefore the start of exactly one sequence.

Formally: each number `x` in `numSet` can be visited by the `while` loop at most once — when the outer `for` loop processes `x - (x's position in its sequence)` (the sequence start). Since no number is ever the starting point of two sequences, and each number is visited at most once by the inner `while`, the total work across all `while` iterations across the entire `for` loop is O(n).

More concisely: the total number of `while` loop iterations across all outer `for` iterations is bounded by `|numSet|`, because each element of the set is incremented over at most once. Combined with the O(n) outer loop, total work = O(n) + O(n) = **O(n)**.

**Space complexity: O(n)** — the `Set` stores at most `n` distinct elements.

**The amortized argument:** This is the same reasoning as why building a `Set` and iterating it is O(n) — even though there's a nested structure, the total number of inner operations is bounded by `n`, not `n²`.

---

## SECTION D: LINKED LISTS (25 marks)

---

### Q10. Linked List Reversal — Pointer Overwrite — (10 marks)

#### (a) Trace for `1 → 2 → 3 → 4 → 5`

**Before loop starts:**
- `prev = null`, `curr = node(1)`, list: `1→2→3→4→5`

**Iteration 1:**
```
curr.next = prev         → node(1).next = null      ← node(1) is now disconnected from node(2)!
prev = curr              → prev = node(1)
curr = curr.next         → curr = null              ← curr.next was just overwritten to null
```
After iteration 1: `prev = node(1)`, `curr = null`. Loop exits immediately.
**Result returned:** `node(1)` — a single-node list `[1]`. All other nodes are lost.

#### (b) The bug

```javascript
curr.next = prev;   // Overwrites the only reference to the rest of the list
// ...
curr = curr.next;   // curr.next is now prev (null or the previously reversed node), not the original next
```

The `next` pointer of `curr` is overwritten before it is saved. The reference to the remainder of the original list is permanently lost.

#### (c) Corrected function

```javascript
function reverseList(head) {
  let prev = null;
  let curr = head;

  while (curr !== null) {
    const nextNode = curr.next;   // Fix: save next BEFORE overwriting
    curr.next = prev;
    prev = curr;
    curr = nextNode;              // advance using saved reference
  }

  return prev;
}
```

**Trace for `1→2→3→4→5` with fix:**
```
Start: prev=null, curr=1
Iter 1: next=2, 1.next=null, prev=1, curr=2
Iter 2: next=3, 2.next=1,    prev=2, curr=3
Iter 3: next=4, 3.next=2,    prev=3, curr=4
Iter 4: next=5, 4.next=3,    prev=4, curr=5
Iter 5: next=null, 5.next=4, prev=5, curr=null
Return: prev=5  →  5→4→3→2→1  ✓
```

---

### Q11. Floyd's Cycle Detection — Wrong Start — (8 marks)

#### (a) The bug and which input causes a crash

```javascript
let fast = head.next;   // Bug — crashes when head is null
```

**Input that causes a crash:** an empty list (`head = null`).

`head.next` throws `TypeError: Cannot read properties of null (reading 'next')` immediately before the loop begins.

Even on a non-null single-node list with no cycle: `head = node(1), node(1).next = null`. Then `fast = null`. Loop condition `slow !== fast` → `node(1) !== null` → true. Inside: `fast === null` → return false. This returns correctly, but only by coincidence.

**The real correctness problem:** By starting `slow = head` and `fast = head.next`, the two pointers begin one step apart. On a list with a cycle, the algorithm still converges (the invariant still holds), but the termination condition `slow !== fast` relies on them starting unequal. If `head` is null, `fast = head.next` crashes. If `head` points to itself (single-node cycle), then `slow = head`, `fast = head.next = head` → `slow === fast` is immediately true, and the loop never runs, returning `true` — which is correct — but for the wrong reason.

#### (b) Why the original (first version) is correct

```javascript
let slow = head;
let fast = head;
while (fast !== null && fast.next !== null) {
  slow = slow.next;
  fast = fast.next.next;
  if (slow === fast) return true;
}
return false;
```

- Both pointers start at `head`. `head = null` is handled safely by the `while` condition before any pointer dereference.
- Each iteration moves `slow` one step and `fast` two steps.
- If there is no cycle, `fast` reaches `null` and the loop exits normally.
- If there is a cycle, `fast` gains on `slow` by one node per iteration within the cycle. They will meet within at most cycle-length iterations — mathematically guaranteed.
- The meeting check `if (slow === fast)` is placed *after* advancing both, avoiding the false positive of them both starting at the same node.

#### (c) Floyd's guarantee, time and space complexity

**Guarantee:** If a cycle exists, `slow` and `fast` will meet within `O(n)` steps, where `n` is the number of nodes. If no cycle exists, `fast` reaches `null` in `O(n)` steps.

**Time complexity:** O(n) — in the worst case, both pointers traverse the list a constant number of times.

**Space complexity:** O(1) — only two pointer variables are used, regardless of list size. This is the key advantage over the `Set`-based approach, which uses O(n) space.

---

### Q12. Merge Two Sorted Lists — Wrong Return — (7 marks)

#### (a) The bug

```javascript
return dummy;   // WRONG — returns the dummy sentinel node, not the actual head
```

`dummy` is a placeholder node with value `0` that was never part of either input list. Returning it means the merged list starts with a spurious `0` node.

#### (b) What `dummy` represents and what to return

`dummy` is a sentinel head node — a convenience node that allows the merge loop to treat the first real node the same as all subsequent nodes (no special case for initialising the head of the result). It is not a real element.

The actual merged list starts at `dummy.next`. That is what must be returned.

#### (c) Corrected return statement and explanation of the dummy node pattern

```javascript
return dummy.next;   // Fix: skip the sentinel, return first real node
```

**Why the dummy node pattern is useful:**

Without a dummy node, the merge loop must special-case the very first node to initialise the result head:

```javascript
// Without dummy — awkward
let head = null, curr = null;
if (l1.val <= l2.val) { head = l1; curr = l1; l1 = l1.next; }
else                  { head = l2; curr = l2; l2 = l2.next; }
// ... then the general loop
```

With a dummy node, the loop body is uniform from the first iteration — `curr.next = ...` always has a valid `curr` to write to. The dummy is discarded at the end via `dummy.next`. This pattern applies to any linked list problem where you build a new list (e.g., merge k sorted lists, partition list, remove duplicates).

---

## MARK SUMMARY

| Q | Topic | Max | Notes |
|---|---|---|---|
| Q1 | Merge sort — two bugs | 10 | Bug 1: slice(mid+1) → slice(mid). Bug 2: missing right remainder loop |
| Q2 | Quick sort — infinite recursion | 8 | pivotIdx → pivotIdx - 1 in left recursive call |
| Q3 | Top-K frequent — complexity | 7 | O(n + m log m); bucket sort O(n); Object.keys integer ordering gotcha |
| Q4 | Binary search first occurrence | 9 | low = mid+1 → high = mid-1 |
| Q5 | Rotated array search | 9 | Correct for no-duplicates; fails with duplicates — add nums[low]==nums[mid] guard |
| Q6 | Binary search on answer | 7 | high = mid-1 → high = mid |
| Q7 | Hash table — 3 bugs | 12 | append(k,v) → append((k,v)); ord(c) → hash(key); no resize guard |
| Q8 | LRU cache | 8 | Separate update path (if/else if) to avoid incorrect eviction check |
| Q9 | Consecutive sequence complexity | 5 | O(n) — each element visited by inner while at most once (amortized) |
| Q10 | List reversal — pointer loss | 10 | Save curr.next before overwriting curr.next |
| Q11 | Floyd's cycle — wrong start | 8 | fast = head.next crashes on null; correct version starts both at head |
| Q12 | Merge lists — wrong return | 7 | return dummy.next, not dummy |
| **Total** | | **100** | |
