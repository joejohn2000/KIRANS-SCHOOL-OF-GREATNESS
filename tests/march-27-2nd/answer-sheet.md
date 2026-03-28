# ANSWER SHEET | MARCH 27 RETEST DAY 11-12 RECOVERY GATE
**Date:** March 27, 2026  
**Topics:** Stack precision, queue using two stacks, monotonic stack tracing, BST complexity, and bounds-based BST validation  
**Total Marks:** 70  

---

## SECTION A: STACK AND QUEUE PRECISION (30 marks)

### Q1. Stack Precision Check (10 marks)

**Model answer:**

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(item) {
    this.items.push(item);
  }

  peek() {
    return this.items[this.items.length - 1];
  }

  size() {
    return this.items.length;
  }
}
```

**Why `push(1)` is wrong:**
- It ignores the function parameter and always stores the constant `1`.
- The method must use the value passed by the caller.

**Complexity:**
- `push`: O(1)
- `peek`: O(1)
- `size`: O(1)

**Suggested marking:**
- methods correct: 7
- explanation of `push(1)` issue: 1
- complexities correct: 2

---

### Q2. Queue Using Two Stacks - Recovery Gate (20 marks)

**Model answer:**

```javascript
class MyQueue {
  constructor() {
    this.inStack = [];
    this.outStack = [];
  }

  push(x) {
    this.inStack.push(x);
  }

  moveIfNeeded() {
    if (this.outStack.length === 0) {
      while (this.inStack.length > 0) {
        this.outStack.push(this.inStack.pop());
      }
    }
  }

  pop() {
    this.moveIfNeeded();
    return this.outStack.pop();
  }

  peek() {
    this.moveIfNeeded();
    return this.outStack[this.outStack.length - 1];
  }

  empty() {
    return this.inStack.length === 0 && this.outStack.length === 0;
  }
}
```

**Explanation:**
- Elements move from `inStack` to `outStack` only when `outStack` is empty and we need the queue front.
- Each element is moved at most once from `inStack` to `outStack`, so even though one operation can trigger a bulk transfer, the average cost per operation is amortized O(1).

**Suggested marking:**
- `push`: 2
- transfer logic: 5
- `pop`: 4
- `peek`: 3
- `empty`: 2
- explanation: 4

---

## SECTION B: MONOTONIC STACK TRACE (12 marks)

### Q3. Daily Temperatures Recovery Check (12 marks)

**Part A - Output:**

```javascript
[1, 1, 4, 2, 1, 1, 0, 0]
```

**Part B - Stack trace for indices 0 through 5**

Write stack as `index:value`.

- after index 0: `[0:73]`
- after index 1: `[1:74]`
- after index 2: `[2:75]`
- after index 3: `[2:75, 3:71]`
- after index 4: `[2:75, 3:71, 4:69]`
- after index 5: `[2:75, 5:72]`

**Part C - Why store indices:**
- We need positions so we can compute the number of days until the next warmer temperature.
- The answer depends on `currentIndex - previousIndex`, not just the temperature values.

**Suggested marking:**
- output: 4
- trace: 4
- indices explanation: 4

---

## SECTION C: BST GATE (28 marks)

### Q4. BST Complexity And Degeneration (10 marks)

**Model answer:**
- In a balanced BST, search, insert, and delete are O(log n).
- In a badly unbalanced BST, search, insert, and delete become O(n).
- A sorted insertion pattern causes degeneration.
- Example: inserting `[1, 2, 3, 4, 5]` in order creates a skewed tree.

**Suggested marking:**
- balanced complexity: 3
- unbalanced complexity: 3
- degeneration pattern: 2
- concrete example: 2

---

### Q5. Validate BST With Bounds (18 marks)

**Part A - Failing tree example:**

```text
    10
   /  \
  5    15
      /  \
     6    20
```

This is invalid because `6` is in the right subtree of `10`, so it must be greater than `10`, but it is not.

**Part B - Corrected solution:**

```javascript
function isValidBST(root) {
  function dfs(node, low, high) {
    if (node === null) return true;

    if ((low !== null && node.val <= low) || (high !== null && node.val >= high)) {
      return false;
    }

    return dfs(node.left, low, node.val) && dfs(node.right, node.val, high);
  }

  return dfs(root, null, null);
}
```

**Part C - Complexity:**
- Time: O(n), because each node is visited once.
- Space: O(h), because recursion uses stack space proportional to tree height.
- Worst case: O(n) space on a skewed tree; balanced case: O(log n).

**Suggested marking:**
- failing tree: 4
- corrected code: 10
- time and space with justification: 4

---

## INTERPRETATION

- This retest should only be considered a pass if the queue code is working, the monotonic-stack trace is correct, and the BST explanation / validation are both solid.
- A good score with a broken `MyQueue` or broken `isValidBST` should still be treated as incomplete recovery.
