# MARCH 30 ASSESSMENT | CUMULATIVE REVIEW THROUGH DAY 19
**Date:** March 30, 2026  
**Focus:** Fresh assessment covering Day 11 through Day 19 after the weekend review  
**Total Marks:** 100  
**Time Allowed:** 120 minutes  

---

> "Fresh prompts, same standards. Transfer the pattern, not the memory of an old answer."

---

## Instructions

1. Answer in JavaScript unless a question explicitly says otherwise.
2. No blanks allowed. If you are unsure, write your best attempt and explain your reasoning.
3. If a question asks for complexity, justify it. Writing only `O(n)` or `O(log n)` is not enough.
4. For implementation questions, write working code, not pseudocode.
5. Before submitting each coding answer, mentally test one normal case and one edge case.
6. Many of these prompts are fresh on purpose. Do not expect them to match the earlier papers.

---

## SECTION A: DAYS 11-13 TRANSFER CHECK (36 marks)

### Q1. Browser History Using Stacks (Day 11) - 12 marks

Implement a browser history manager using stacks.

```javascript
class BrowserHistory {
  constructor(homepage) {
    // TODO
  }

  visit(url) {
    // TODO
  }

  back(steps) {
    // TODO
  }

  forward(steps) {
    // TODO
  }
}
```

Requirements:
- `visit(url)` goes to a new page and clears the forward history
- `back(steps)` moves back up to `steps` times and returns the current page
- `forward(steps)` moves forward up to `steps` times and returns the current page

After your code:
- explain why stacks are a natural fit here
- state the time complexity of `visit`, `back`, and `forward`

---

### Q2. Lowest Common Ancestor In A BST (Day 12) - 10 marks

Implement:

```javascript
function lowestCommonAncestor(root, p, q) {
  // TODO
}
```

Assume `root`, `p`, and `q` are nodes in the same BST.

Then answer:
1. Why does the BST property let you avoid searching both subtrees?
2. What is the time complexity in a balanced BST vs a badly unbalanced BST?

---

### Q3. Binary Search On Answer + Top-K Reasoning (Day 13) - 14 marks

**Part A (10 marks):**  
Implement:

```javascript
function shipWithinDays(weights, days) {
  // TODO
}
```

Return the smallest ship capacity needed to ship all packages within `days`.

Example:
- `weights = [3, 2, 2, 4, 1, 4]`
- `days = 3`
- answer: `6`

**Part B (2 marks):**  
Explain why this is a binary-search-on-answer problem. Your explanation must mention:
- the search space
- the yes/no check
- why a successful check moves `high = mid`

**Part C (2 marks):**  
Without writing full code, explain how a bucket-based `topKFrequent` solution can avoid sorting all keys and still reach `O(n)`.

---

## SECTION B: DAYS 14-17 CORE APPLICATION (44 marks)

### Q4. Graph Representation + LRU Reasoning (Day 14) - 10 marks

Given the directed edges:

```javascript
const edges = [
  [0, 1],
  [0, 2],
  [1, 3],
  [2, 4],
  [3, 5],
  [4, 5]
];
```

**Part A (6 marks):**
1. Write the adjacency list.
2. Starting from node `0`, write the BFS visit order.
3. Why is a queue the correct data structure for BFS?

**Part B (4 marks):**  
In a `Map`-based LRU cache, why is this update wrong for an existing key?

```javascript
map.set(key, value);
```

Explain why the correct pattern is:

```javascript
map.delete(key);
map.set(key, value);
```

---

### Q5. Build Order With Topological Sort (Day 15) - 12 marks

Implement:

```javascript
function findBuildOrder(numTasks, deps) {
  // TODO
}
```

Rules:
- `deps` contains pairs `[task, prerequisite]`
- return one valid build order
- return `[]` if there is a cycle

Example:
- `numTasks = 5`
- `deps = [[1,0],[2,0],[3,1],[3,2],[4,3]]`
- one valid answer is `[0,1,2,3,4]`

Before your code, write 2-3 sentences describing:
- what data structures you will use
- why the algorithm works
- the time complexity

---

### Q6. Min Cost Climbing Stairs (Day 16) - 12 marks

Before your code, write the recurrence relation in one sentence.

Then implement:

```javascript
function minCostClimbingStairs(cost) {
  // TODO
}
```

You may solve it with memoization or tabulation, but your solution must be real working code.

After your code:
- state the time complexity
- state the space complexity
- briefly explain why this is a DP problem

---

### Q7. Permutation In String (Day 17) - 10 marks

Implement:

```javascript
function checkInclusion(s1, s2) {
  // TODO
}
```

Return `true` if some permutation of `s1` appears as a substring of `s2`, otherwise return `false`.

Examples:
- `checkInclusion("ab", "eidbaooo")` -> `true`
- `checkInclusion("ab", "eidboaoo")` -> `false`

After your code:
1. Explain why the sliding window length stays fixed at `s1.length`.
2. State the time and space complexity with justification.

---

## SECTION C: DAYS 18-19 PRECISION AND EXPLANATION (20 marks)

### Q8. Missing Number Using XOR Only (Day 18) - 10 marks

Implement:

```javascript
function missingNumber(nums) {
  // TODO
}
```

Rules:
- the numbers are in the range `[0, n]`
- exactly one number is missing
- use XOR, not sorting and not a hash set

After your code:
1. Show the XOR trace for `nums = [3, 0, 1]`
2. Explain why the algorithm works
3. State the time and space complexity with justification

---

### Q9. Wallet And CashbackWallet (Day 19) - 10 marks

Implement the following classes:

```javascript
class Wallet {
  constructor(owner, balance = 0) {
    // TODO
  }

  deposit(amount) {
    // TODO
  }

  spend(amount) {
    // TODO
  }

  getBalance() {
    // TODO
  }
}

class CashbackWallet extends Wallet {
  applyCashback(percent) {
    // TODO
  }
}
```

Requirements:
- `deposit(amount)` adds money
- `spend(amount)` throws an error if `amount > balance`
- `getBalance()` returns the current balance
- `applyCashback(percent)` increases the balance by that percentage

Then answer:
1. Why is `CashbackWallet` still substitutable anywhere a `Wallet` is expected?
2. Give one concrete example of an LSP violation in a subclass design.

---

## SCORING GUIDE

| Score | Interpretation |
|---|---|
| 85-100 | Strong transfer across the widened scope |
| 70-84 | Good progress, but keep carry-over on weaker days |
| 55-69 | Partial transfer; needs narrower follow-up before widening again |
| Below 55 | Not ready for broader advancement yet |

---

*This paper is intentionally broader than the last few gates. It checks whether focused recovery now transfers across fresh Day 11-19 prompts.*
