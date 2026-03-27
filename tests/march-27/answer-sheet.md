# ANSWER SHEET | MARCH 27 DAY 11-12 CHECKPOINT
**Date:** March 27, 2026  
**Topics:** Stacks, Queues, Trees, and BSTs  
**Total Marks:** 100  

---

## SECTION A: STACKS AND QUEUES - IMPLEMENTATION FIRST (45 marks)

### Q1. Build a Stack Correctly (15 marks)

**Model answer:**

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(item) {
    this.items.push(item);
  }

  pop() {
    return this.items.pop();
  }

  peek() {
    return this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }
}
```

**Complexities:**
- `push`: O(1)
- `pop`: O(1)
- `peek`: O(1)
- `isEmpty`: O(1)
- `size`: O(1)

**Why `items.peek()` fails:**
- JavaScript arrays do not have a built-in `.peek()` method.
- Calling `items.peek()` would try to call `undefined` as a function, which throws a `TypeError`.
- The correct top element access pattern is `items[items.length - 1]`.

**Suggested marking:**
- Core methods correct: 10
- `peek()` correct on empty stack: 2
- Complexities correct: 2
- `.peek()` explanation correct: 1

---

### Q2. Implement Queue Using Two Stacks (18 marks)

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

**Why `pop()` is amortized O(1):**
- A single `pop()` can trigger a transfer from `inStack` to `outStack`, which costs O(n) for that moment.
- But each element is moved from `inStack` to `outStack` at most once, and later popped at most once.
- Over many operations, the total work per element stays constant on average, so the amortized cost per queue operation is O(1).

**Suggested marking:**
- `push` correct: 2
- transfer logic correct: 5
- `pop` correct: 4
- `peek` correct: 3
- `empty` correct: 2
- amortized explanation correct: 2

---

### Q3. Monotonic Stack Pattern - Daily Temperatures (12 marks)

**Part A - Output:**

```javascript
[1, 1, 4, 2, 1, 1, 0, 0]
```

**Part B - Stack trace for indices 0 through 5**

Write stack as `index:value`.

- after index 0 (`73`): `[0:73]`
- after index 1 (`74`): `[1:74]`
- after index 2 (`75`): `[2:75]`
- after index 3 (`71`): `[2:75, 3:71]`
- after index 4 (`69`): `[2:75, 3:71, 4:69]`
- after index 5 (`72`): `[2:75, 5:72]`

Explanation of index 5:
- `72` is warmer than `69`, so pop index 4 and answer for index 4 is `5 - 4 = 1`
- `72` is warmer than `71`, so pop index 3 and answer for index 3 is `5 - 3 = 2`
- `72` is not warmer than `75`, so stop and push index 5

**Part C - Why store indices:**
- We need to compute the number of days until a warmer temperature.
- That means we need the distance `currentIndex - previousIndex`.
- If we stored only temperatures, we would lose the positions and could not compute the answer.

**Suggested marking:**
- output array: 4
- trace mostly correct: 4
- indices explanation: 4

---

## SECTION B: TREES AND BSTS - EXPLAIN FIRST (55 marks)

### Q4. Tree Traversal Drill (12 marks)

Given tree:

```text
        8
      /   \
     4     12
    / \    / \
   2   6  10  14
```

**Answers:**
- pre-order: `8, 4, 2, 6, 12, 10, 14`
- in-order: `2, 4, 6, 8, 10, 12, 14`
- post-order: `2, 6, 4, 10, 14, 12, 8`
- level-order: `8, 4, 12, 2, 6, 10, 14`

**Why in-order is sorted here:**
- This is a BST, so every left subtree contains smaller values and every right subtree contains larger values.
- In-order traversal visits `left -> node -> right`, which therefore lists the BST values in sorted order.

**Suggested marking:**
- four traversals correct: 8
- BST explanation correct: 4

---

### Q5. BST Complexity Under Pressure (10 marks)

**Model answer:**
- In a balanced BST, search, insert, and delete are all O(log n) because each step cuts the remaining search space roughly in half.
- In a badly unbalanced BST, those operations become O(n) because the tree behaves like a linked list.
- A sorted insertion pattern can cause this degeneration.
- Example: inserting `[1, 2, 3, 4, 5]` in that order creates a right-skewed tree.

**Suggested marking:**
- balanced complexities: 3
- unbalanced complexities: 3
- degeneration pattern named: 2
- concrete example: 2

---

### Q6. Maximum Depth of Binary Tree (13 marks)

**Model approach (example):**
- I will use recursion. For each node, the maximum depth is `1 + max(depth of left subtree, depth of right subtree)`.
- If the node is `null`, the depth is `0`. I visit each node once, so time is O(n), and the recursive call stack is O(h), where `h` is the tree height.

**Model code:**

```javascript
function maxDepth(root) {
  if (root === null) {
    return 0;
  }

  const leftDepth = maxDepth(root.left);
  const rightDepth = maxDepth(root.right);

  return 1 + Math.max(leftDepth, rightDepth);
}
```

**Complexity:**
- Time: O(n), because every node is visited once.
- Space: O(h), because the recursion stack grows with the tree height.

**Suggested marking:**
- approach stated before code: 3
- base case correct: 2
- recursive structure correct: 5
- time and space justified: 3

---

### Q7. Validate BST - Debug and Fix (20 marks)

#### Part A - Why the original solution is wrong

The buggy solution only compares each node with its immediate children.  
That is not enough for BST validation, because every node in the entire left subtree must be less than the root, and every node in the entire right subtree must be greater than the root.

**Failing example:**

```text
    10
   /  \
  5    15
      /  \
     6    20
```

- `6` is in the right subtree of `10`, so it should be greater than `10`
- but the buggy solution only checks `6 < 15`, which looks fine locally
- it incorrectly returns `true`

#### Part B - Corrected implementation

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

#### Part C - Complexity

- Time: O(n), because each node is checked once.
- Space: O(h), because the recursion stack depends on the tree height.
- In the worst case of a skewed tree, `h = n`; in a balanced tree, `h = log n`.

**Suggested marking:**
- precise bug explanation: 6
- corrected code: 10
- complexity and justification: 4

---

## OVERALL INTERPRETATION

- Strong performance here means the student can both implement Day 11 structures and explain Day 12 tree logic clearly.
- Weak performance on Section A means implementation fluency is still lagging.
- Weak performance on Section B means the student needs more explain-first tree/BST practice before advancing further.
