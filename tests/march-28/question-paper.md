# MARCH 28 ASSESSMENT | FINAL RECOVERY GATE BEFORE DAY 13
**Date:** March 28, 2026  
**Focus:** Exact `MyQueue` correctness, exact Daily Temperatures trace, BST complexity wording, and typo-free bounds-based `isValidBST`  
**Total Marks:** 60  
**Time Allowed:** 55 minutes  

---

> "Almost correct is still wrong. This test is about exactness."

---

## Instructions

1. Answer in JavaScript.
2. No blanks allowed.
3. This is the final recovery gate before Day 13. It is intentionally narrow.
4. For Q1 and Q4, write working code, not pseudocode.
5. For Q2 and Q3, answer in complete sentences.
6. If you mention complexity, justify it briefly.

---

## SECTION A: QUEUE EXACTNESS (22 marks)

### Q1. Perfect `MyQueue` (22 marks)

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

After the code, explain in 2-3 sentences:
- when values move from `inStack` to `outStack`
- why `pop()` is amortized O(1)

Important:
- use exact property names
- use exact method calls
- `peek()` must return the queue front

---

## SECTION B: MONOTONIC STACK TRACE (14 marks)

### Q2. Daily Temperatures - Exact Trace (14 marks)

Given:

```javascript
const temperatures = [73, 74, 75, 71, 69, 72, 76, 73];
```

Answer all 3:

**Part A (4 marks):**  
Write the final output array.

**Part B (6 marks):**  
Trace the stack after processing indices `0` through `5`.  
Write the stack as indices or as `index:value`.

**Part C (4 marks):**  
Why must the stack store indices instead of temperatures?

---

## SECTION C: BST COMPLEXITY PRECISION (8 marks)

### Q3. Balanced vs Unbalanced BST (8 marks)

Answer in complete sentences:

1. What is the time complexity of search / insert / delete in a balanced BST?
2. What is the time complexity of search / insert / delete in a badly unbalanced BST?
3. What insertion pattern causes degeneration?
4. Give one concrete insertion sequence.

---

## SECTION D: BOUNDS-BASED BST VALIDATION (16 marks)

### Q4. Clean `isValidBST` Pass (16 marks)

The following local-child-check solution is wrong:

```javascript
function isValidBST(root) {
  if (!root) return true;

  if (root.left && root.left.val >= root.val) return false;
  if (root.right && root.right.val <= root.val) return false;

  return isValidBST(root.left) && isValidBST(root.right);
}
```

**Part A (4 marks):**  
Give one real failing tree where this returns the wrong answer.

**Part B (8 marks):**  
Write a typo-free solution using min/max bounds.

**Part C (4 marks):**  
State the time complexity and the space complexity.  
For space, use `O(h)` and also explain the worst case.

---

## PASS RULE

This paper should only count as a true pass if all of these are correct:
- `MyQueue` works exactly
- the Daily Temperatures output and trace are exact
- `isValidBST` is typo-free and uses a real failing counterexample

---

## SCORING GUIDE

| Score | Interpretation |
|---|---|
| 48-60 | Recovery gate passed; okay to begin Day 13 carry-over |
| 38-47 | Partial recovery; one more narrow fix before Day 13 |
| Below 38 | Recovery gate not cleared; repeat targeted recovery |

---

*This is the last narrow gate. Pass this cleanly before widening scope.*
