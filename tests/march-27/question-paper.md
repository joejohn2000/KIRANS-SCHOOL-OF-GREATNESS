# MARCH 27 ASSESSMENT | DAY 11-12 CHECKPOINT
**Date:** March 27, 2026  
**Focus:** Primarily Day 11 and Day 12 - Stacks, Queues, Trees, and Binary Search Trees  
**Total Marks:** 100  
**Time Allowed:** 100 minutes  

---

> "Do not leave blanks. A partial attempt is always better than silence."

---

## Instructions

1. Answer in JavaScript.
2. No blanks allowed. If you are unsure, write your best attempt and explain your reasoning.
3. **Section A is implementation-first**: write the code before writing the explanation.
4. **Section B is explain-first**: for every implementation question in Section B, write 2-3 sentences describing your approach before writing code.
5. If a question asks for complexity, justify it. Writing only `O(n)` or `O(log n)` is not enough.
6. Before moving on, mentally test one normal case and one edge case.

---

## SECTION A: STACKS AND QUEUES - IMPLEMENTATION FIRST (45 marks)

### Q1. Build a Stack Correctly (15 marks)

Implement the class below. Do not use any fake `.peek()` method on arrays.

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(item) {
    // TODO
  }

  pop() {
    // TODO
  }

  peek() {
    // TODO
  }

  isEmpty() {
    // TODO
  }

  size() {
    // TODO
  }
}
```

Requirements:
- `push(item)` adds an item to the top of the stack
- `pop()` removes and returns the top item
- `peek()` returns the top item without removing it
- `isEmpty()` returns `true` if the stack has no items
- `size()` returns the number of items
- `peek()` should return `undefined` for an empty stack

After writing the code:
- state the time complexity of each method
- explain why `items.peek()` would fail in JavaScript

---

### Q2. Implement Queue Using Two Stacks (18 marks)

Implement a queue using two stacks.

```javascript
class MyQueue {
  constructor() {
    this.inStack = [];
    this.outStack = [];
  }

  push(x) {
    // TODO
  }

  pop() {
    // TODO
  }

  peek() {
    // TODO
  }

  empty() {
    // TODO
  }
}
```

Requirements:
- `push(x)` pushes element `x` to the back of the queue
- `pop()` removes and returns the element at the front of the queue
- `peek()` returns the front element
- `empty()` returns `true` when the queue is empty

After your code:
- explain why `pop()` is **amortized O(1)** and not `O(n)` for every operation

---

### Q3. Monotonic Stack Pattern - Daily Temperatures (12 marks)

Given:

```javascript
const temperatures = [73, 74, 75, 71, 69, 72, 76, 73];
```

For LeetCode #739 Daily Temperatures:

**Part A (4 marks):**  
Write the correct output array.

**Part B (4 marks):**  
Trace the stack state after processing the first 6 indices (`0` through `5`).  
You may write stack entries as indices or as `index:value`.

**Part C (4 marks):**  
Explain why the stack should store **indices** instead of only temperatures.

---

## SECTION B: TREES AND BSTS - EXPLAIN FIRST (55 marks)

### Q4. Tree Traversal Drill (12 marks)

Consider this BST:

```text
        8
      /   \
     4     12
    / \    / \
   2   6  10  14
```

Write:
- pre-order traversal
- in-order traversal
- post-order traversal
- level-order traversal

Then answer:
- Why does the in-order traversal come out sorted for this tree?

---

### Q5. BST Complexity Under Pressure (10 marks)

Answer in complete sentences:

1. What is the time complexity of **search**, **insert**, and **delete** in a **balanced BST**?
2. What is the time complexity of those same operations in a **badly unbalanced BST**?
3. What specific insertion pattern can cause a BST to degenerate into `O(n)` performance?
4. Give one concrete example sequence that causes that degeneration.

---

### Q6. Maximum Depth of Binary Tree (13 marks)

Before writing code, write 2-3 sentences explaining:
- your approach
- time complexity
- space complexity

Then implement:

```javascript
function maxDepth(root) {
  // TODO
}
```

Assume the usual node shape:

```javascript
class TreeNode {
  constructor(val, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}
```

---

### Q7. Validate BST - Debug and Fix (20 marks)

The following solution is **wrong**:

```javascript
function isValidBST(root) {
  if (!root) return true;

  if (root.left && root.left.val >= root.val) return false;
  if (root.right && root.right.val <= root.val) return false;

  return isValidBST(root.left) && isValidBST(root.right);
}
```

**Part A (6 marks):**  
Explain exactly why this is wrong. Give a concrete tree where this function returns the wrong answer.

**Part B (10 marks):**  
Before writing code, write 2-3 sentences describing your fix strategy. Then write a corrected implementation.

**Part C (4 marks):**  
State the time and space complexity, and justify both.

---

## SCORING GUIDE

| Score | Level | Recommendation |
|---|---|---|
| 90-100 | Strong | Ready to move on with light review |
| 80-89 | Good | Advance, but keep 1 carry-over weakness |
| 70-79 | Borderline pass | Advance carefully with multiple carry-over checks |
| Below 70 | Not ready | Repeat weak areas before advancing |

---

*This paper is designed to test both code-writing and explanation discipline. Day 11 requires implementation strength. Day 12 requires explanation-first thinking. This assessment checks both.*
