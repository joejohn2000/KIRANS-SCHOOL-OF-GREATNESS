# APRIL 6 ASSESSMENT | CUMULATIVE REVIEW DAYS 1–20
**Date:** April 6, 2026
**Focus:** Full cumulative review — foundations through system design, refactoring, and design patterns
**Total Marks:** 100
**Time Allowed:** 120 minutes

---

> "Fresh prompts. Same standards. Transfer the pattern, not the memory of the last answer."

---

## Instructions

1. All code in JavaScript unless stated otherwise.
2. **No blanks.** A broken attempt with a clear explanation of where it breaks scores more than an empty box.
3. For every coding question: write your approach in 1–2 sentences **before** writing any code.
4. After writing any class or constructor, check that every property name you declared matches every place you use it.
5. Complexity justification is required — writing only `O(n)` without a reason scores zero for that part.
6. Before submitting any method, trace it with one normal input and one edge case in your head.

---

## SECTION A: FOUNDATIONS — Days 1–9 (25 marks)

### Q1. Closures and Scope (10 marks)

**Part A (4 marks):** Predict the exact output of this code. Explain why each line produces the value it does.

```javascript
function makeCounter(start) {
  let count = start;
  return {
    increment() { count++; },
    decrement() { count--; },
    value()     { return count; }
  };
}

const a = makeCounter(10);
const b = makeCounter(0);

a.increment();
a.increment();
b.increment();

console.log(a.value());
console.log(b.value());
console.log(a === b);
```

**Part B (4 marks):** This code does not behave as intended. Fix it **two ways**: once using `let`, once using an IIFE closure. Both fixes must produce `0, 1, 2, 3, 4`.

```javascript
const fns = [];
for (var i = 0; i < 5; i++) {
  fns.push(function() { return i; });
}

console.log(fns[0]()); // prints 5, expected 0
console.log(fns[1]()); // prints 5, expected 1
console.log(fns[2]()); // prints 5, expected 2
console.log(fns[3]()); // prints 5, expected 3
console.log(fns[4]()); // prints 5, expected 4
```

**Part C (2 marks):** In one sentence each:
1. Why does the original code print `5` five times instead of `0, 1, 2, 3, 4`?
2. Why does the `let` fix work?

---

### Q2. Big O Complexity (5 marks)

For each snippet, state the **time complexity** and **space complexity**. One sentence of justification is required for each. The label alone scores zero.

**Snippet A:**
```javascript
function hasPair(arr, target) {
  const seen = new Set();
  for (const n of arr) {
    if (seen.has(target - n)) return true;
    seen.add(n);
  }
  return false;
}
```

**Snippet B:**
```javascript
function allPairs(arr) {
  const result = [];
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      result.push([arr[i], arr[j]]);
    }
  }
  return result;
}
```

**Snippet C:**
```javascript
function countBits(n) {
  let count = 0;
  while (n > 0) {
    count += n & 1;
    n >>= 1;
  }
  return count;
}
```

---

### Q3. Hash Map — Group Anagrams (10 marks)

Implement:

```javascript
function groupAnagrams(words) {
  // TODO
}
```

Group words that are anagrams of each other. Words in the same group share exactly the same set of characters and frequencies.

Examples:
- `groupAnagrams(["eat","tea","tan","ate","nat","bat"])` → `[["eat","tea","ate"],["tan","nat"],["bat"]]`
- `groupAnagrams([""])` → `[[""]]`
- `groupAnagrams(["a"])` → `[["a"]]`

Requirements:
- Use a `Map` where the key identifies the anagram group
- Handle the edge cases above
- State time and space complexity with justification

After your code: in two sentences, explain what you chose as the map key and why it correctly identifies anagram groups.

---

## SECTION B: CORE DATA STRUCTURES & ALGORITHMS — Days 10–17 (45 marks)

### Q4. Trees and Queues (15 marks)

**Part A — Level-Order Traversal (8 marks)**

Implement:

```javascript
function levelOrder(root) {
  // TODO
  // Return an array of arrays: each inner array contains the values at one level.
}
```

Given this tree:
```
        5
       / \
      3   8
     / \   \
    1   4   9
```
Expected output: `[[5], [3, 8], [1, 4, 9]]`

After your code:
- State time and space complexity with justification.
- In two sentences, explain why a queue (not a stack) produces level-order (not depth-first) output.

**Part B — Validate a BST (7 marks)**

Implement:

```javascript
function isValidBST(root) {
  // TODO
}
```

Rules:
- All nodes in the left subtree are **strictly less than** the current node's value.
- All nodes in the right subtree are **strictly greater than** the current node's value.
- This must hold for **every** node, not just immediate children.

After your code: draw or describe a tree that would **pass** a check of only immediate children but **fail** a correct BST validation. Explain what your implementation catches that the naive check misses.

---

### Q5. Graph — BFS and Topological Sort (15 marks)

**Part A — BFS Traversal (4 marks)**

Given this adjacency list:
```javascript
const graph = {
  A: ["B", "C"],
  B: ["D"],
  C: ["D", "E"],
  D: ["F"],
  E: ["F"],
  F: []
};
```

1. Write the BFS visit order starting from `"A"`. Show the queue state at each step.
2. In one sentence: why does BFS guarantee shortest-path order in an unweighted graph?

**Part B — Topological Sort (11 marks)**

Implement:

```javascript
function buildOrder(numTasks, deps) {
  // TODO
}
```

- `deps` contains pairs `[task, prerequisite]` — `task` cannot start before `prerequisite`
- Return one valid order to complete all tasks
- Return `[]` if there is a cycle

Example:
- `numTasks = 6`
- `deps = [[2,0],[3,1],[4,2],[4,3],[5,4]]`
- One valid answer: `[0, 1, 2, 3, 4, 5]`

**Before your code:** describe the algorithm in 3 sentences — name the two data structures it uses and what role each plays.

**After your code:** trace the in-degree array and queue contents for the example above, step by step through each dequeue.

---

### Q6. Dynamic Programming and Sliding Window (15 marks)

**Part A — House Robber (8 marks)**

A robber targets a row of houses. Adjacent houses share a security connection — robbing two neighbours triggers an alarm. Each element in `nums` is the amount of money in that house.

Implement:

```javascript
function rob(nums) {
  // TODO
}
```

Examples:
- `rob([1, 2, 3, 1])` → `4` (rob index 0 and 2: 1+3)
- `rob([2, 7, 9, 3, 1])` → `12` (rob index 0, 2, 4: 2+9+1)

**Before your code:** write the recurrence relation in one line. (e.g. `dp[i] = ...`)

**After your code:**
- State time and space complexity with justification.
- In two sentences, explain why greedy (always rob the larger neighbour) does not always work. Give a counterexample.

**Part B — Sliding Window Explanation (7 marks)**

This question is written — no code required.

You are given `nums = [3, 1, 4, 1, 5, 9, 2, 6]` and `k = 3`.

1. Walk through the sliding window approach step by step to find the maximum sum of any 3 consecutive elements. Show the window position and running sum at each step.
2. What is the window invariant? When exactly does the window slide?
3. State the time and space complexity. Justify both.
4. Without writing code: how would you adapt this fixed-window approach to a **variable** window that finds the longest substring without repeating characters? Name the one key difference.

---

## SECTION C: OOP, REFACTORING AND DESIGN PATTERNS — Days 18–20 (20 marks)

### Q7. OOP and Refactoring (10 marks)

Read this code carefully.

```javascript
class ReportGenerator {
  generate(report) {
    // Validate
    if (!report.title) throw new Error("Missing title");
    if (!report.data || report.data.length === 0) throw new Error("No data");

    // Format data
    let output = `=== ${report.title} ===\n`;
    for (const row of report.data) {
      output += `${row.label}: ${row.value}\n`;
    }

    // Apply discount display
    if (report.type === "sales") output += "Type: Sales Report\n";
    if (report.type === "finance") output += "Type: Finance Report\n";
    if (report.type === "hr") output += "Type: HR Report\n";

    // Output
    console.log(output);
    fs.writeFileSync(`${report.title}.txt`, output);
    sendToSlack(output);

    return output;
  }
}
```

**Part A (4 marks):** Identify **two** code smells in this code. For each smell:
- Name the catalog category
- Name the specific smell
- Name the exact refactoring technique that fixes it

**Part B (6 marks):** Refactor `ReportGenerator`. Apply both techniques from Part A. After refactoring:
- The class must not contain type-switching logic
- Adding a new report type must not require modifying `ReportGenerator`
- The output responsibilities (console, file, Slack) must be separated from the formatting logic

---

### Q8. Design Pattern — Observer (10 marks)

An online store fires events when an order is placed. Multiple services must react:
- `InventoryService`: logs `[Inventory] Reducing stock for order #<id>`
- `EmailService`: logs `[Email] Confirmation sent for order #<id>`
- `AnalyticsService`: logs `[Analytics] Order #<id> recorded`

Implement the **Observer** pattern:

```javascript
class OrderSystem {
  constructor() {
    // TODO
  }

  subscribe(observer) {
    // TODO
  }

  unsubscribe(observer) {
    // TODO
  }

  placeOrder(orderId) {
    // TODO — notify all subscribers
  }
}
```

Requirements:
1. Each observer has a `notify(orderId)` method.
2. Implement all three concrete observer classes.
3. Write a usage example: subscribe all three, place order `101`, then unsubscribe `EmailService`, then place order `102`. Show the expected output for both orders.

**After your code:**
- Map each participant name (Subject, ConcreteSubject, Observer, ConcreteObserver) to your implementation.
- In one sentence: why does `OrderSystem` not need to import or reference `InventoryService` directly?

---

## SECTION D: SYSTEM DESIGN — Day 20 (10 marks)

### Q9. System Design Concepts (10 marks)

**Part A — CAP Theorem (4 marks)**

Explain the CAP theorem in 2–3 sentences. Then complete this table with a real database for each pair and a one-sentence justification:

| Pair | What it sacrifices | Real database example | One-sentence justification |
|---|---|---|---|
| CP | | | |
| AP | | | |
| CA | | | |

**Part B — Caching (3 marks)**

Your API serves a product catalogue. Products are read 10,000 times per second but updated at most once per hour.

1. Name the caching pattern you would use.
2. Describe what happens on a cache miss in that pattern.
3. Name one situation where caching this data would cause a real problem and explain why.

**Part C — Rate Limiter (3 marks)**

Implement a working rate limiter. Max `N` requests per `W` milliseconds per user. Prune old timestamps on every call.

```javascript
class RateLimiter {
  constructor(maxRequests, windowMs) {
    // TODO
  }

  allow(userId) {
    // TODO — return true or false
  }
}
```

After your code: state time and space complexity with one sentence each.

---

## SCORING GUIDE

| Score | Interpretation |
|---|---|
| 85–100 | Strong transfer across all 20 days — ready to advance to Phase 4 |
| 70–84 | Good overall — advance with targeted carry-over on weakest section |
| 55–69 | Partial transfer — one section needs focused remediation before widening |
| Below 55 | Not ready to advance — repeat weakest two sections before Day 21 |

---

*All prompts are fresh. Do not expect them to match previous test papers. Transfer the approach, not the memory of a past answer.*
