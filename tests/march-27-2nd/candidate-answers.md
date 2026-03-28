# CANDIDATE ANSWERS | MARCH 27 RETEST DAY 11-12 RECOVERY GATE
**Evaluation Date:** March 28, 2026  
**Source:** Provided in chat / terminal on March 28, 2026  
**Answer in:** JavaScript  

---

## Q1. Stack Precision Check

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(item) {
    this.items.push(item);
  }

  peek() {
    if (this.isEmpty()) {
      return "overflow";
    }
    return this.item[this.items.length - 1];
  }

  size() {
    if (this.isEmpty()) {
      return "overflow";
    }
    return this.items.length - 1;
  }
}
```

The main reason for not allowing `push(1)` is because it will only return `1` instead of item passed through item.

Time complexity of `push`, `peek` and `size` is `O(1)`.

---

## Q2. Queue Using Two Stacks

```javascript
class MyQueue {
  constructor() {
    this.inStack = [];
    this.outStack = [];
  }

  push(x) {
    this.instack.push(x);
  }

  pop() {
    this.peek();
    return this.outStack.pop();
  }

  peek() {
    if (this.outStack.length == 0) {
      while (this.inStack.length > 0) {
        this.outStack.push(this.inStack.pop);
      }
    }
  }

  empty() {
    return this.inStack.length === 0 && this.outStack.length === 0;
  }
}
```

Values move from `inStack` to `outStack` only when `outstack` is empty and push and pop is called.

`pop()` is amortized `O(1)` since each item is moved exactly once.

---

## Q3. Daily Temperatures Recovery Check

```javascript
function temp(temperatures) {
  let results = new Array(temperatures.length).fill(0);
  let temps = [];

  for (let i = 0; i < temperatures.length; i++) {
    while (temps.length > 0 && temperatures[i] > temperatures[temps[temps.length - 1]]) {
      const j = temps.pop();
      results[j] = i - j;
    }
    temps.push(i);
  }
  return results;
}
```

The stack stores in indices as problems requires to store days between the warmer climate instead of seeing how cold it is the only way to do this is by storing indices indicating the climate rather than storing temperatures.

Input:

```javascript
const temperatures = [73, 74, 75, 71, 69, 72, 76, 73];
```

Final output array: `[1,1,4,2,0,1,0,0]`

Trace provided:
- `i = 0`, `temperatures[0] = 73`, since stack is empty push `i`, stack = `[73]`, result = `[0,0,0,0,0,0,0,0]`
- `i = 1`, `temperatures[1] = 74`, since `74 > 73`, stack = `[74]`, result = `[1,0,0,0,0,0,0,0]`
- `i = 2`, `temperatures[2] = 75`, since `75 > 73`, stack = `[75]`, result = `[1,1,0,0,0,0,0,0]`
- `i = 3`, `temperatures[3] = 71`, since not greater just push, stack = `[71,75]`
- `i = 4`, `temperatures[4] = 69`, since not greater just push, stack = `[69,71,75]`
- `i = 5`, `temperatures[5] = 72`, since not greater just push, stack = `[72,69,71,75]`

---

## Q4. BST Complexity And Degeneration

Time complexity of search / insert / delete in a balanced BST is `O(logn)`.

Time complexity of search / insert / delete in a badly unbalanced BST is `O(n)`.

Degeneration occurs if nodes are arranged in sorted order either increasing or decreasing. If it arranged like this this would have either left branch or right branch and this will act like linked list.

Example tree given:

```text
      10
     /
    20
   /
  30
 /
40
/
50
```

---

## Q5. Validate BST With Bounds

Failing tree example given:

```text
        20
      /    \
    10      50
           /  \
          40   60
```

Explanation:
This code is failing as it only checks the sub tree condition and right side should be greater than left side but when taking whole code the node is 20 which is less than 40 on right side so based on the code it will show true but in reality its false.

```javascript
function isValidBST(root, min = -Infinity, max = Infinity) {
  if (!root) return true;
  if (root.val < min || rol.val > max) {
    return false;
  }
  return isValidBST(root.left, min, root.val) && isValidBST(root.right, root.val, max);
}
```

Time complexity is `O(n)`.

Space complexity is `O(n)`.
