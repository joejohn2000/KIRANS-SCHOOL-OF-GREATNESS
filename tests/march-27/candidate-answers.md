# CANDIDATE ANSWERS | MARCH 27 DAY 11-12 CHECKPOINT
**Date:** March 27, 2026  
**Source:** Transcribed from `tests/march-27/candidate-answer.md` for canonical post-submission evaluation  
**Answer in:** JavaScript  

---

## Q1. Build a Stack Correctly

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(item) {
    this.items.push(1);
  } // O(1)

  pop() {
    if (this.isEmpty()) return "Underflow";
    return this.items.pop();
  } // O(n)

  peek() {
    return this.items[this.items.length - 1];
  } // O(1)

  isEmpty() {
    return this.items.length === 0;
  } // O(1)

  size() {
    return this.items.length;
  } // O(1)
}
```

This would fail in js because syntax for peek is not created.

---

## Q2. Implement Queue Using Two Stacks

```javascript
class MyQueue {
  constructor() {
    this.inStack = [];
    this.outStack = [];
  }

  push(x) {
    this.items.push(1);
  }

  pop() {
    this.peek();
    return this.pop(outStack);
  }

  peek() {
    if (this.outStack.length === 0) {
      while (this.inStack.length > 0) {
        this.outStack.push(this.inStack.pop());
      }
    }
    return this.outStack[this.outStack.length - 1];
  }

  empty() {
    return this.s1.length === 0 && this.s2.length === 0;
  }
}
```

`pop()` is amortized O(1) and not O(n) for every operation as it just returns the array with finding last element and deleting it.

---

## Q3. Daily Temperatures

```javascript
function temp(temperatures) {
  let results = new Array().fill(0);
  let temps = [];

  for (let i = 0; i < temperatures.length; i++) {
    while (temps.length > 0 && temperatures[i] > temperatures[temps[temps.length - 1]]) {
      const j = temps.pop;
      results[j] = i - j;
    }
    temps.push(i);
  }
  return results;
}
```

Results should be `[1,1,4,2,1,1,0]`.

After processing the indices 6 it checks the next value if its length > 0 and the next value which is 77 is greater than the one stored in temp array since it is the case it pops the value from temp stack and nothing is changed in results array.

It stores indices instead of temperatures to compare it with other values in array.

---

## Q4. Tree Traversal Drill

- pre-order traversal (Root-left-right) - `[8,4,2,6,12,10,14]`
- in-order traversal (left-root-right) - `[2,4,6,8,10,12,14]`
- post-order traversal (left-right-root) - `[2, 6, 4, 10, 14, 12, 8]`
- level-order traversal - `[8,4,12,2,6,10,14]`

Because the tree is created in order that left node root and right are increasing as it goes up.

---

## Q5. BST Complexity Under Pressure

Time complexity of:
- Search - `O(nlogn)`
- Insert, delete - `O(n)`

For every badly unbalanced BST it becomes `O(n^2)`.

If insertion pattern is

---

## Q6. Maximum Depth of Binary Tree

If `!root` means there is no data in the tree so we can return 0 since the size is 0 and this is the base function telling recursion to stop. Now we can take length from max of recursively checking length if right or left comparing which one is the biggest of them then repeat till it reach the end and the final product will be return back from function.

Time complexity is `O(n)`.

Space complexity is `O(n)`.

```javascript
function maxDepth(root) {
  if (!root) return 0;
  return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

---

## Q7. Validate BST - Debug and Fix

To fix the code u need min and max which will dynamically check during each interaction.

```javascript
function isValidBST(root, min, max) {
  if (!root) return true;

  if (min != null && node.val <= min || max != null && nod.val >= max) return false;

  return isValidBST(root.left, min, max) && isValidBST(root.right, min, max);
}
```

The old code returns false as it only checks if the values just under are greater than the current node so in order to check if the tree is valid binary search tree u need to check all the nodes.

Time complexity is `O(n)`.

---

## Source Note

The original source file contained a trailing `8.` with no answer, but the paper has only 7 questions.
