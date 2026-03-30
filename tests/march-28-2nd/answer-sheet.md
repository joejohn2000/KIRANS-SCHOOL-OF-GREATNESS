# ANSWER SHEET | MARCH 28 ASSESSMENT THROUGH DAY 13
**Date:** March 28, 2026  
**Topics:** Stacks, queues, trees, BSTs, binary search on answer, hash tables, and bucket-based top-K thinking  
**Total Marks:** 100  

---

## SECTION A: STACKS AND QUEUES - FRESH APPLICATIONS (25 marks)

### Q1. Min Stack Implementation (15 marks)

**Model answer:**

```javascript
class MinStack {
  constructor() {
    this.stack = [];
    this.minStack = [];
  }

  push(val) {
    this.stack.push(val);
    if (this.minStack.length === 0 || val <= this.minStack[this.minStack.length - 1]) {
      this.minStack.push(val);
    }
  }

  pop() {
    const removed = this.stack.pop();
    if (removed === this.minStack[this.minStack.length - 1]) {
      this.minStack.pop();
    }
    return removed;
  }

  top() {
    return this.stack[this.stack.length - 1];
  }

  getMin() {
    return this.minStack[this.minStack.length - 1];
  }
}
```

**Why `getMin()` is O(1):**
- A second stack keeps track of the minimum values seen so far.
- The current minimum is always at the top of `minStack`, so `getMin()` returns it in constant time.

**Suggested marking:**
- stack structure and methods: 11
- correct min tracking: 3
- explanation: 1

---

### Q2. Recent Counter Using a Queue (10 marks)

**Model answer:**

```javascript
class RecentCounter {
  constructor() {
    this.q = [];
  }

  ping(t) {
    this.q.push(t);

    while (this.q.length > 0 && this.q[0] < t - 3000) {
      this.q.shift();
    }

    return this.q.length;
  }
}
```

**Why a queue fits:**
- Requests arrive in time order.
- Old requests are removed from the front, and new requests are added at the back, which matches queue behavior.

**Suggested marking:**
- working code: 8
- queue explanation: 2

---

## SECTION B: TREES AND BSTS - FRESH QUESTIONS (25 marks)

### Q3. Level Order Traversal and Queue Reasoning (10 marks)

**Answer:**
- level-order traversal: `7, 3, 11, 1, 5, 13`

**Why a queue is natural:**
- Level-order traversal visits nodes in first-in, first-out order by level.
- A queue lets us process the current node, then place its children at the back so they are visited in the correct breadth-first order.

**Suggested marking:**
- traversal: 4
- explanation: 6

---

### Q4. Insert Into BST (15 marks)

**Model answer:**

```javascript
function insertIntoBST(root, val) {
  if (root === null) {
    return { val, left: null, right: null };
  }

  if (val < root.val) {
    root.left = insertIntoBST(root.left, val);
  } else {
    root.right = insertIntoBST(root.right, val);
  }

  return root;
}
```

**Where `13` goes:**
- `13 > 8`, so go right to `10`
- `13 > 10`, so go right to `14`
- `13 < 14`, so it becomes the left child of `14`

**Complexity:**
- balanced BST: O(log n)
- badly unbalanced BST: O(n)

**Suggested marking:**
- implementation: 9
- insertion trace: 3
- complexity: 3

---

## SECTION C: DAY 13 CARRY-OVER + HEAPS THINKING (50 marks)

### Q5. Binary Search on Answer - Smallest Divisor (20 marks)

**Model answer:**

```javascript
function smallestDivisor(nums, threshold) {
  let low = 1;
  let high = Math.max(...nums);

  function canFit(divisor) {
    let total = 0;
    for (const num of nums) {
      total += Math.ceil(num / divisor);
    }
    return total <= threshold;
  }

  while (low < high) {
    const mid = Math.floor((low + high) / 2);

    if (canFit(mid)) {
      high = mid;
    } else {
      low = mid + 1;
    }
  }

  return low;
}
```

**Why this is binary search on answer:**
- We are not searching an array index; we are searching the answer space of possible divisors.
- If a divisor works, then any larger divisor also works, which gives the monotonic condition binary search needs.

**Time complexity:**
- O(n log m), where `n` is the length of `nums` and `m` is the maximum value in `nums`

**Suggested marking:**
- correct binary search structure: 12
- helper logic: 4
- explanation and complexity: 4

---

### Q6. Hash Table With Chaining - Bug Fix (15 marks)

**Two real bugs:**

1. `new Array(size).fill([])` makes every bucket reference the same array.
2. `_hash` returns `total` directly without reducing it into the table range, so indices can go out of bounds.

**Why they break it:**
- With shared bucket arrays, pushing into one bucket affects every bucket.
- Without `% this.size`, the index can be larger than the table length.

**Corrected version:**

```javascript
class HashTable {
  constructor(size = 5) {
    this.size = size;
    this.table = Array.from({ length: size }, () => []);
  }

  _hash(key) {
    let total = 0;
    for (const ch of key) total += ch.charCodeAt(0);
    return total % this.size;
  }

  set(key, value) {
    const index = this._hash(key);
    const bucket = this.table[index];

    for (let i = 0; i < bucket.length; i++) {
      if (bucket[i][0] === key) {
        bucket[i][1] = value;
        return;
      }
    }

    bucket.push([key, value]);
  }
}
```

**Suggested marking:**
- bug 1 identified/explained: 4
- bug 2 identified/explained: 4
- corrected class: 7

---

### Q7. Top K Frequent Elements - Bucket Thinking (15 marks)

**Model answer:**

```javascript
function topKFrequent(nums, k) {
  const freq = new Map();

  for (const num of nums) {
    freq.set(num, (freq.get(num) || 0) + 1);
  }

  const buckets = Array.from({ length: nums.length + 1 }, () => []);

  for (const [num, count] of freq.entries()) {
    buckets[count].push(num);
  }

  const result = [];
  for (let i = buckets.length - 1; i >= 0 && result.length < k; i--) {
    for (const num of buckets[i]) {
      result.push(num);
      if (result.length === k) break;
    }
  }

  return result;
}
```

**Why bucket thinking can reach O(n):**
- Counting frequencies takes O(n).
- Filling buckets also takes O(n) overall.
- Scanning buckets from high frequency to low takes O(n), so we avoid the O(n log n) cost of sorting all keys.

**Suggested marking:**
- frequency map: 4
- bucket construction: 4
- result collection: 4
- explanation: 3

---

## OVERALL INTERPRETATION

- Strong performance here means the student is no longer only recovering old weak spots but can transfer the ideas to fresh questions.
- Weak performance on Section C means Day 13 carry-over is still not stable enough.
