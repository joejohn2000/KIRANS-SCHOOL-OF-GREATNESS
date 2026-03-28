# MARCH 28 ASSESSMENT | CONTENT THROUGH DAY 13
**Date:** March 28, 2026  
**Focus:** Fresh questions covering Day 11, Day 12, and Day 13 content  
**Total Marks:** 100  
**Time Allowed:** 95 minutes  

---

> "Same skills, new questions. Solve the pattern, not the memory of the old paper."

---

## Instructions

1. Answer in JavaScript unless a question explicitly says otherwise.
2. These are new questions. Do not rely on memory from earlier tests; reason them out.
3. No blanks allowed.
4. If a question asks for complexity, justify it briefly.
5. For implementation questions, write working code, not pseudocode.

---

## SECTION A: STACKS AND QUEUES - FRESH APPLICATIONS (25 marks)

### Q1. Min Stack Implementation (15 marks)

Implement a stack that supports retrieving the minimum element in O(1) time.

```javascript
class MinStack {
  constructor() {
    // TODO
  }

  push(val) {
    // TODO
  }

  pop() {
    // TODO
  }

  top() {
    // TODO
  }

  getMin() {
    // TODO
  }
}
```

Requirements:
- `push(val)` pushes a value
- `pop()` removes the top value
- `top()` returns the top value
- `getMin()` returns the minimum value currently in the stack

After the code:
- explain how your design keeps `getMin()` at O(1)

---

### Q2. Recent Counter Using a Queue (10 marks)

Design a class `RecentCounter`:

```javascript
class RecentCounter {
  constructor() {
    // TODO
  }

  ping(t) {
    // TODO
  }
}
```

Each call `ping(t)` adds a new request at time `t` and returns the number of requests that happened in the inclusive range `[t - 3000, t]`.

Example:
- `ping(1)` -> `1`
- `ping(100)` -> `2`
- `ping(3001)` -> `3`
- `ping(3002)` -> `3`

After the code:
- explain why a queue is the right structure here

---

## SECTION B: TREES AND BSTS - FRESH QUESTIONS (25 marks)

### Q3. Level Order Traversal and Queue Reasoning (10 marks)

Given this tree:

```text
        7
      /   \
     3     11
    / \      \
   1   5      13
```

Answer:

1. Write the level-order traversal.
2. Explain why a queue is the natural data structure for level-order traversal.

---

### Q4. Insert Into BST (15 marks)

Write a function to insert a value into a BST and return the root.

```javascript
function insertIntoBST(root, val) {
  // TODO
}
```

Then answer:

1. If you start with this BST:

```text
      8
     / \
    3   10
       /  \
      9    14
```

and insert `13`, where does it go?

2. What is the time complexity in a balanced BST vs a badly unbalanced BST?

---

## SECTION C: DAY 13 CARRY-OVER + HEAPS THINKING (50 marks)

### Q5. Binary Search on Answer - Smallest Divisor (20 marks)

You are given an array of positive integers `nums` and an integer `threshold`.

Choose a positive integer divisor `d`. For each number in `nums`, divide it by `d`, round up, and sum the results.

Return the smallest divisor `d` such that the total is less than or equal to `threshold`.

Write:

```javascript
function smallestDivisor(nums, threshold) {
  // TODO
}
```

Example:
- `nums = [1, 2, 5, 9]`, `threshold = 6`
- answer: `5`

After the code:
- explain why this is a binary-search-on-answer problem
- state the time complexity

---

### Q6. Hash Table With Chaining - Bug Fix (15 marks)

This JavaScript hash table has bugs:

```javascript
class HashTable {
  constructor(size = 5) {
    this.size = size;
    this.table = new Array(size).fill([]);
  }

  _hash(key) {
    let total = 0;
    for (const ch of key) total += ch.charCodeAt(0);
    return total;
  }

  set(key, value) {
    const index = this._hash(key);
    this.table[index].push([key, value]);
  }
}
```

Tasks:

1. Identify **two real bugs**.
2. Explain why each bug breaks the hash table.
3. Write a corrected version of the class.

You only need `constructor`, `_hash`, and `set`.

---

### Q7. Top K Frequent Elements - Bucket Thinking (15 marks)

Write a function:

```javascript
function topKFrequent(nums, k) {
  // TODO
}
```

Return the `k` most frequent elements.

Example:
- `topKFrequent([1,1,1,2,2,3], 2)` -> `[1,2]`

Rules:
- do **not** sort all keys by frequency
- solve it using frequency counting plus buckets

After the code:
- explain why the bucket idea can reach O(n)

---

## SCORING GUIDE

| Score | Interpretation |
|---|---|
| 85-100 | Strong; ready to continue beyond Day 13 carry-over |
| 70-84 | Good, but keep carry-over on weaker topics |
| 55-69 | Partial understanding; needs more focused review |
| Below 55 | Not ready to widen scope yet |

---

*This paper uses all-new questions, but it still measures the same core skills. Transfer the pattern, not the exact old answer.*
