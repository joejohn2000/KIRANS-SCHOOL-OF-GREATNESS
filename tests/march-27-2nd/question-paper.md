# MARCH 27 RETEST | DAY 11-12 RECOVERY GATE
**Date:** March 27, 2026  
**Focus:** Stack / Queue precision, Monotonic Stack reasoning, BST complexity, and bounds-based BST validation  
**Total Marks:** 70  
**Time Allowed:** 60 minutes  

---

> "This is not a new-topic test. This is a recovery gate. Pass the weak spots before moving on."

---

## Instructions

1. Answer in JavaScript.
2. No blanks allowed.
3. This paper is narrow on purpose. It checks the exact things that failed in the earlier March 27 checkpoint.
4. If a question asks for complexity, justify it briefly.
5. For Q2 and Q5, write working code, not pseudocode.
6. For Q4, answer in complete sentences.

---

## SECTION A: STACK AND QUEUE PRECISION (30 marks)

### Q1. Stack Precision Check (10 marks)

Complete the missing methods correctly:

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(item) {
    // TODO
  }

  peek() {
    // TODO
  }

  size() {
    // TODO
  }
}
```

Then answer:
- Why is `push(1)` wrong if the requirement is `push(item)`?
- What is the time complexity of `push`, `peek`, and `size`?

---

### Q2. Queue Using Two Stacks - Recovery Gate (20 marks)

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

After your code, explain in 2-3 sentences:
- when values move from `inStack` to `outStack`
- why `pop()` is amortized O(1)

---

## SECTION B: MONOTONIC STACK TRACE (12 marks)

### Q3. Daily Temperatures Recovery Check (12 marks)

Given:

```javascript
const temperatures = [73, 74, 75, 71, 69, 72, 76, 73];
```

Answer all 3:

**Part A (4 marks):**  
Write the final output array.

**Part B (4 marks):**  
Trace the stack after processing indices `0` through `5`.  
You may write entries as indices or `index:value`.

**Part C (4 marks):**  
Why must the stack store indices instead of only temperatures?

---

## SECTION C: BST GATE (28 marks)

### Q4. BST Complexity And Degeneration (10 marks)

Answer in complete sentences:

1. What is the time complexity of search / insert / delete in a balanced BST?
2. What is the time complexity of search / insert / delete in a badly unbalanced BST?
3. What insertion pattern causes degeneration?
4. Give one concrete example sequence.

---

### Q5. Validate BST With Bounds (18 marks)

The following solution is wrong:

```javascript
function isValidBST(root) {
  if (!root) return true;

  if (root.left && root.left.val >= root.val) return false;
  if (root.right && root.right.val <= root.val) return false;

  return isValidBST(root.left) && isValidBST(root.right);
}
```

**Part A (4 marks):**  
Give one concrete failing tree where this returns the wrong answer.

**Part B (10 marks):**  
Write a correct solution using min/max bounds.

**Part C (4 marks):**  
State the time and space complexity and justify both.

---

## SCORING GUIDE

| Score | Interpretation |
|---|---|
| 56-70 | Recovery gate passed; okay to continue with carry-over |
| 45-55 | Partial recovery; repeat the missed weak spots before full Day 13 work |
| Below 45 | Recovery gate failed; repeat the focus session before moving on |

---

*This retest is intentionally focused. Passing this matters more than broad coverage right now.*
