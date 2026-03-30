# ANSWER SHEET | MARCH 28 FINAL RECOVERY GATE
**Date:** March 28, 2026  
**Topics:** Queue exactness, monotonic stack trace, BST complexity precision, and clean bounds-based BST validation  
**Total Marks:** 60  

---

## SECTION A: QUEUE EXACTNESS (22 marks)

### Q1. Perfect `MyQueue` (22 marks)

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
- Values move from `inStack` to `outStack` only when `outStack` is empty and we need the queue front.
- Each element is transferred at most once from `inStack` to `outStack`, so although one call can trigger a bulk move, the average cost per operation is amortized O(1).

**Suggested marking:**
- `push`: 3
- transfer helper / transfer logic: 5
- `pop`: 4
- `peek`: 4
- `empty`: 2
- explanation: 4

---

## SECTION B: MONOTONIC STACK TRACE (14 marks)

### Q2. Daily Temperatures - Exact Trace (14 marks)

**Part A - Output:**

```javascript
[1, 1, 4, 2, 1, 1, 0, 0]
```

**Part B - Stack trace after indices 0 through 5**

Write stack as `index:value`.

- after index 0: `[0:73]`
- after index 1: `[1:74]`
- after index 2: `[2:75]`
- after index 3: `[2:75, 3:71]`
- after index 4: `[2:75, 3:71, 4:69]`
- after index 5: `[2:75, 5:72]`

**Part C - Why store indices:**
- We need indices so we can compute the number of days until the next warmer temperature.
- The answer depends on `currentIndex - previousIndex`, not just the temperature values.

**Suggested marking:**
- output: 4
- trace: 6
- explanation: 4

---

## SECTION C: BST COMPLEXITY PRECISION (8 marks)

### Q3. Balanced vs Unbalanced BST (8 marks)

**Model answer:**
- In a balanced BST, search, insert, and delete are O(log n).
- In a badly unbalanced BST, search, insert, and delete are O(n).
- Degeneration happens when values are inserted in sorted order.
- Example sequence: `[1, 2, 3, 4, 5]`.

**Suggested marking:**
- balanced complexity: 2
- unbalanced complexity: 2
- degeneration pattern: 2
- concrete sequence: 2

---

## SECTION D: BOUNDS-BASED BST VALIDATION (16 marks)

### Q4. Clean `isValidBST` Pass (16 marks)

**Part A - Real failing tree example:**

```text
    10
   /  \
  5    15
      /  \
     6    20
```

The local-child-check solution wrongly returns `true` here because `6 < 15` looks locally valid, but `6` is in the right subtree of `10` and should therefore be greater than `10`.

**Part B - Typo-free bounds solution:**

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
- Time: O(n), because each node is checked once.
- Space: O(h), because recursion uses stack space proportional to tree height.
- Worst case: O(n) space for a skewed tree.
- Balanced case: O(log n) space.

**Suggested marking:**
- failing tree: 4
- corrected code: 8
- time and space with worst-case note: 4

---

## INTERPRETATION

- This paper should be treated as passed only if the queue code is exact, the monotonic-stack trace is exact, and the BST validation is typo-free.
- A good score with a broken `MyQueue` or broken `isValidBST` should still be treated as incomplete recovery.
