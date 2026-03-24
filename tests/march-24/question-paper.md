# DEBUG & SOLVE — HARD ASSESSMENT
**Date:** March 24, 2026
**Focus:** Days 7–10 — Sorting, Binary Search, Hash Tables (Deep Dive), Linked Lists
**Total Marks:** 100
**Time Allowed:** 90 minutes

---

> *"A bug is never where you think it is. Look at the thing that calls the thing."*

---

**Instructions:**
1. Every question contains broken, incorrect, or subtly flawed code. Your job is to find the bug(s) AND provide the corrected version.
2. For debug questions: state **(a) what the bug is**, **(b) why it causes the observed behaviour**, **(c) the fixed code**.
3. For solve questions: state **(a) your approach**, **(b) time and space complexity**, **(c) the implementation**.
4. No partial credit for identifying the bug without fixing it, or fixing it without explaining why.
5. Complexity analysis is mandatory wherever requested — wrong complexity = marks deducted.

---

## SECTION A: SORTING (25 marks)

---

### Q1. The Merge Sort That Loses Data (10 marks)

The following merge sort implementation has **two bugs**. It sometimes produces incorrect output and occasionally drops elements.

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;

  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid + 1));  // Bug 1

  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let i = 0, j = 0;

  while (i < left.length && j < right.length) {
    if (left[i] < right[j]) {
      result.push(left[i]);
      i++;
    } else {
      result.push(right[j]);
      j++;
    }
  }

  while (i < left.length) {
    result.push(left[i]);
    i++;
  }
  // Bug 2 — remainder of right is never appended

  return result;
}
```

**Test case:** `mergeSort([5, 2, 8, 1, 9, 3])` — what does it currently return (trace through the first split to show why), and what should it return?

**(a)** Identify both bugs precisely.
**(b)** Explain what incorrect behaviour each bug causes.
**(c)** Write the fully corrected implementation.

---

### Q2. The Quick Sort That Hangs (8 marks)

This quick sort runs forever on certain inputs.

```javascript
function quickSort(arr, low = 0, high = arr.length - 1) {
  if (low < high) {
    const pivotIdx = partition(arr, low, high);
    quickSort(arr, low, pivotIdx);       // Bug
    quickSort(arr, pivotIdx + 1, high);
  }
  return arr;
}

function partition(arr, low, high) {
  const pivot = arr[high];
  let i = low - 1;

  for (let j = low; j < high; j++) {
    if (arr[j] <= pivot) {
      i++;
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
  }
  [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]];
  return i + 1;
}
```

**(a)** Identify the bug.
**(b)** Explain which class of inputs triggers infinite recursion and why. Give a concrete example.
**(c)** Write the corrected line.

---

### Q3. Complexity Analysis Under Pressure (7 marks)

A candidate wrote this function to find the **k most frequent elements** in an array:

```javascript
function topKFrequent(nums, k) {
  const freq = {};
  for (const n of nums) {
    freq[n] = (freq[n] || 0) + 1;
  }

  return Object.keys(freq)
    .sort((a, b) => freq[b] - freq[a])
    .slice(0, k)
    .map(Number);
}
```

**(a)** State the time complexity of this solution and justify it.
**(b)** This solution is correct but not optimal. Describe how you would improve it to O(n) using bucket sort. You do not need to write code — a precise description is sufficient.
**(c)** JavaScript's `Object.keys()` has a subtle ordering behaviour that can silently cause this function to return a wrong answer under a specific condition. Identify that condition, explain exactly why it causes incorrect output, and fix it with one change.

---

## SECTION B: BINARY SEARCH (25 marks)

---

### Q4. The Binary Search With an Off-by-One (9 marks)

This binary search is supposed to return the **index of the first occurrence** of `target` in a sorted array with duplicates. It has a bug.

```javascript
function firstOccurrence(arr, target) {
  let low = 0, high = arr.length - 1;
  let result = -1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);

    if (arr[mid] === target) {
      result = mid;
      low = mid + 1;   // Bug
    } else if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return result;
}
```

**Test case:** `firstOccurrence([1, 2, 2, 2, 3], 2)` — what does it currently return, and what should it return? (Remember: arrays are 0-indexed.)

**(a)** Identify the bug.
**(b)** Explain why it finds *some* occurrence of `target` but not the *first* one.
**(c)** Write the corrected line.

---

### Q5. The Rotated Array Search That Cuts the Wrong Half (9 marks)

This solution for searching in a rotated sorted array (LeetCode #33) produces wrong answers on some inputs.

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
      if (target > nums[mid] && target <= nums[low]) {   // Bug
        low = mid + 1;
      } else {
        high = mid - 1;
      }
    }
  }

  return -1;
}
```

**Test case:** `search([6, 7, 0, 1, 2, 3, 4], 6)` — trace through and show where it goes wrong.

**(a)** Trace the execution of the test case step by step.
**(b)** Identify the bug. Explain why the wrong variable is used and what it should be instead.
**(c)** Write the corrected implementation. State its time complexity.

---

### Q6. Binary Search on Answer (7 marks)

You are given a sorted array `piles` where `piles[i]` is the number of bananas in pile `i`. A guard returns in `h` hours. You want to find the **minimum eating speed `k`** (bananas per hour) such that you can finish all piles within `h` hours. Each hour you pick one pile and eat at most `k` bananas from it.

The following solution has a logic error:

```javascript
function minEatingSpeed(piles, h) {
  let low = 1, high = Math.max(...piles);

  while (low < high) {
    const mid = Math.floor((low + high) / 2);

    if (canFinish(piles, mid, h)) {
      high = mid - 1;   // Bug
    } else {
      low = mid + 1;
    }
  }

  return low;
}

function canFinish(piles, speed, h) {
  let hours = 0;
  for (const pile of piles) {
    hours += Math.ceil(pile / speed);
  }
  return hours <= h;
}
```

**(a)** Identify the bug and explain what happens when `canFinish` returns `true` for a speed that is not the minimum.
**(b)** Write the corrected line.
**(c)** Explain why `low = high` is the correct invariant for this "binary search on answer" pattern, and state the time complexity.

> Verify your understanding: `minEatingSpeed([4, 9, 4], 9)` should return `2`. What does the buggy version return and why?

---

## SECTION C: HASH TABLES — DEEP DIVE (25 marks)

---

### Q7. The Broken Hash Table Implementation (12 marks)

A candidate implemented a basic hash table with chaining. It has **three bugs** — two subtle, one critical.

```python
class HashTable:
    def __init__(self, size=10):
        self.size = size
        self.table = [[] for _ in range(size)]

    def _hash(self, key):
        return sum(ord(c) for c in key) % self.size

    def set(self, key, value):
        index = self._hash(key)
        bucket = self.table[index]

        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket[i] = (key, value)
                return

        bucket.append(key, value)   # Bug 1 — critical

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
                break

    def load_factor(self):
        total_items = sum(len(b) for b in self.table)
        return total_items / self.size   # Bug 2 — subtle

    def resize(self, new_size):
        old_table = self.table
        self.size = new_size
        self.table = [[] for _ in range(new_size)]   # Bug 3 — subtle

        for bucket in old_table:
            for k, v in bucket:
                self.set(k, v)
```

**(a)** Identify all three bugs precisely.
**(b)** For each bug, explain what goes wrong at runtime.
**(c)** Write the corrected class.

---

### Q8. LRU Cache — The Update That Forgets Its Place (8 marks)

This LRU Cache implementation has a bug in `put` that causes an incorrect eviction when a key is updated.

```javascript
class LRUCache {
  constructor(capacity) {
    this.capacity = capacity;
    this.map = new Map();
  }

  get(key) {
    if (!this.map.has(key)) return -1;
    const val = this.map.get(key);
    this.map.delete(key);
    this.map.set(key, val);
    return val;
  }

  put(key, value) {
    if (this.map.has(key)) {
      this.map.set(key, value);   // Bug — updates value but does not move key to MRU position
      return;
    }
    if (this.map.size >= this.capacity) {
      const lruKey = this.map.keys().next().value;
      this.map.delete(lruKey);
    }
    this.map.set(key, value);
  }
}
```

**Scenario:** `capacity=2`, operations: `put(1,1)`, `put(2,2)`, `put(1,10)`, `put(3,3)`, `get(1)`.

**(a)** Trace through the scenario step by step. Show the state of the map after each operation and identify what the final `get(1)` returns vs what it should return.
**(b)** Identify the bug. Explain why `map.set(key, value)` alone is not sufficient when the key already exists in a `Map`-backed LRU cache.
**(c)** Write the corrected `put` method.

---

### Q9. Longest Consecutive Sequence — Wrong Complexity Claim (5 marks)

```javascript
function longestConsecutive(nums) {
  const numSet = new Set(nums);
  let longest = 0;

  for (const num of numSet) {
    if (!numSet.has(num - 1)) {
      let current = num;
      let length = 1;

      while (numSet.has(current + 1)) {
        current++;
        length++;
      }

      longest = Math.max(longest, length);
    }
  }

  return longest;
}
```

A candidate claims this is O(n²) because of the nested `while` loop inside a `for` loop.

**(a)** Is the candidate correct? Justify your answer rigorously — do NOT just say "it's O(n), trust me."
**(b)** What is the actual time complexity and space complexity? Prove it.

---

## SECTION D: LINKED LISTS (25 marks)

---

### Q10. The Linked List Reversal That Corrupts the List (10 marks)

This iterative linked list reversal has a bug that causes it to either produce the wrong result or lose nodes.

```javascript
class ListNode {
  constructor(val, next = null) {
    this.val = val;
    this.next = next;
  }
}

function reverseList(head) {
  let prev = null;
  let curr = head;

  while (curr !== null) {
    curr.next = prev;   // Bug — next pointer overwritten before saving it
    prev = curr;
    curr = curr.next;
  }

  return prev;
}
```

**Test case:** List `1 → 2 → 3 → 4 → 5`. Trace the first two iterations to show exactly what goes wrong.

**(a)** Trace the first two iterations manually and show the state of `prev`, `curr`, and the list after each.
**(b)** Identify the bug.
**(c)** Write the corrected function.

---

### Q11. Floyd's Cycle Detection — Broken Condition (8 marks)

This implementation of Floyd's tortoise and hare algorithm has a bug that causes it to crash on lists with a cycle.

```javascript
function hasCycle(head) {
  let slow = head;
  let fast = head;

  while (fast !== null && fast.next !== null) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) return true;
  }

  // Bug — falls through here even when cycle exists in some cases
  return false;
}
```

Actually, the above logic is almost correct — but the bug is in **where the pointers start**. The version below has been modified by a candidate and now crashes:

```javascript
function hasCycle(head) {
  let slow = head;
  let fast = head.next;   // Bug

  while (slow !== fast) {
    if (fast === null || fast.next === null) return false;
    slow = slow.next;
    fast = fast.next.next;
  }

  return true;
}
```

**(a)** Identify the bug and explain which input causes a crash.
**(b)** Explain why the original (first version above) is correct and this version is not.
**(c)** State what Floyd's algorithm guarantees and its time and space complexity.

---

### Q12. Merge Two Sorted Lists — The Dummy Node Trap (7 marks)

```javascript
function mergeTwoLists(l1, l2) {
  let dummy = new ListNode(0);
  let curr = dummy;

  while (l1 !== null && l2 !== null) {
    if (l1.val <= l2.val) {
      curr.next = l1;
      l1 = l1.next;
    } else {
      curr.next = l2;
      l2 = l2.next;
    }
    curr = curr.next;
  }

  curr.next = l1 !== null ? l1 : l2;

  return dummy;   // Bug
}
```

**(a)** Identify the bug.
**(b)** Explain what `dummy` represents and what should be returned instead.
**(c)** Write the corrected return statement and explain why the dummy node pattern is useful in linked list problems.

---

## SCORING GUIDE

| Section | Questions | Marks |
|---|---|---|
| A: Sorting | Q1–Q3 | 25 |
| B: Binary Search | Q4–Q6 | 25 |
| C: Hash Tables Deep Dive | Q7–Q9 | 25 |
| D: Linked Lists | Q10–Q12 | 25 |
| **Total** | | **100** |

**Mark allocation per question:**
- Bug identification: 30%
- Explanation of why the bug causes the observed behaviour: 30%
- Corrected code / analysis: 40%

---

*Read carefully. Every bug was written to look plausible. If the code looks fine at a glance, look again.*
