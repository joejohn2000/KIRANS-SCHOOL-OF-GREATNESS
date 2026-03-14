# 30-Day Software Development Fundamentals Mastery Plan

## Profile
- **Languages**: JavaScript, Python (Kotlin dropped)
- **Goal**: FAANG senior engineer level
- **Time**: 5hrs/day — 2hrs learning · 2hrs practice · 1hr review
- **Style**: Dynamic — plan updated daily based on verification results

## Skills Assessment (from evaluation)
| Skill | Status | Notes |
|-------|--------|-------|
| JS var/let/const basics | ⚠️ Partial | Understands basic differences but struggles with scoping implications (closures, hoisting) |
| Python list mutation / pass-by-ref | ⚠️ Partial | Understands basic mutation but confused about references vs copies |
| Basic control flow / FizzBuzz | ✅ Known | Solid grasp of loops and conditionals |
| JS closure & scoping edge cases | ❌ Gap | Significant misunderstanding of closures and lexical scoping |
| Big O / time-space complexity | ❌ Gap | Not assessed in evaluation but identified as critical gap from interview |
| Hash table problem-solving (e.g. Two Sum) | ❌ Gap | Not assessed in evaluation but identified as critical gap from interview |
| Algorithm design (general) | ❌ Gap | Not assessed in evaluation but identified as critical gap from interview |
| Functional programming concepts | ❌ Gap | Unable to implement closures, higher-order functions, or memoization |

## How Verification Gates Work
Each day ends with **two gates**:
- **Coding challenge**: a specific problem to solve
- **Written explanation**: a specific concept question (3–5 sentences)

**Pass both** → move to next day as planned
**Fail one** → carry-over task added to top of next day (max 1hr)
**Fail 2+ consecutive days** → next day becomes a Catch-Up Day (repeat weakest topic, no new content)

---

## Phase 1: Foundations (Days 1–5)
### Focus: Quick review of known ground + closing early gaps

---

### Day 1 — Variables, Types & JS Scoping Edge Cases ⚡ Quick Review
**Objective**: Confirm solid understanding of primitives and JS scoping; identify any gaps

**Learning (2hrs)**
- JS: primitives, type coercion, `typeof`, `==` vs `===`
- Python: `type()`, mutable vs immutable types, `id()`
- JS scoping: `var` (function scope) vs `let`/`const` (block scope)
- Closure mechanics: why `var` in loops captures by reference

**Practice (2hrs)**
- Write 5 JS snippets predicting the output of scoping puzzles (including `var` in `setTimeout` loops)
- Write a Python function that demonstrates the difference between mutating an object vs reassigning a variable
- Fix 3 buggy JS snippets that misuse `var` in loop contexts

**Review (1hr)**
- Document: what surprised you, what was obvious, what was unclear

**Verification Gate**

*Coding challenge*: Fix the following so it prints `0, 1, 2`:
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```
Explain why it currently prints `3, 3, 3` and provide two different fixes.

*Written explanation*: What is the difference between `var`, `let`, and `const` in JavaScript? Describe a real bug that can occur from misusing `var` in a loop.

---

### Day 2 — Control Flow + Functions & Scope
**Objective**: Master loops, conditionals, and function scoping in JS and Python

**Learning (2hrs)**
- JS: `for`, `while`, `for...of`, `for...in`, loop control (`break`/`continue`)
- Python: `for`, `while`, `range()`, list comprehensions
- Functions: declaration vs expression vs arrow functions in JS; `def` in Python
- Scope: local, global, `nonlocal` (Python), closures

**Practice (2hrs)**
- Implement: factorial, Fibonacci, and FizzBuzz (1–100) in both JS and Python
- Write a closure in JS that creates a counter with `increment` and `reset` methods
- Write a Python function using `nonlocal` to maintain state across calls

**Review (1hr)**
- Note the pattern: closures in JS vs closures in Python — how do they differ?

**Verification Gate**

*Coding challenge*: Write a `makeCounter()` function in JavaScript that returns an object with `increment()`, `decrement()`, and `getCount()` methods. The count must persist between calls using a closure (no class, no global variable).

*Written explanation*: Explain what a closure is in your own words. Why does the `makeCounter` solution work without using a class or global variable?

---

### Day 3 — Big O Complexity (MANDATORY before algorithms)
**Objective**: Understand time and space complexity well enough to analyze any code you write

**Learning (2hrs) — Big O block**
- What Big O measures and why it matters
- Common complexities: O(1), O(log n), O(n), O(n log n), O(n²), O(2ⁿ)
- How to derive complexity by reading code (loops, nested loops, recursion)
- Space complexity: stack frames, auxiliary space
- Array operations: O(1) index access, O(n) unsorted search, O(log n) binary search

**Practice (2hrs)**
- For each of 8 given code snippets, write the time and space complexity with explanation
- Rewrite an O(n²) duplicate-finding function to O(n) using a set
- Identify why binary search is O(log n) — write out the reasoning step by step

**Review (1hr)**
- Build a personal Big O cheat sheet in your notes

**Verification Gate**

*Coding challenge*: Given an unsorted array of integers, write a function that returns `true` if any value appears twice. Write it first as O(n²), then refactor to O(n). Label both solutions with their complexity.

*Written explanation*: Explain the difference between O(n) and O(n²). If you had an array of 10,000 elements, approximately how many operations would each perform? Why does this matter for FAANG interviews?

---

### Day 4 — Arrays & List Operations
**Objective**: Master array/list manipulation and common patterns

**Learning (2hrs)**
- JS: `push/pop`, `shift/unshift`, `splice/slice`, `map`, `filter`, `reduce`, `sort`
- Python: `append/pop`, `insert`, list slicing, list comprehensions, `sorted()`
- Two-pointer technique
- Sliding window pattern (intro)

**Practice (2hrs)**
- LeetCode [#26 Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
- LeetCode [#283 Move Zeroes](https://leetcode.com/problems/move-zeroes/)
- LeetCode [#167 Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) (two-pointer)
- Write `flatten(arr)` that flattens one level of nesting without using `.flat()`

**Review (1hr)**
- Write out time complexity for each problem you solved

**Verification Gate**

*Coding challenge*: LeetCode [#121 Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/). Solve it in O(n) time and O(1) space. Explain your approach.

*Written explanation*: What is the two-pointer technique? Describe a problem type where it reduces time complexity compared to a brute-force approach.

---

### Day 5 — Dictionaries, Maps & Hash-Based Thinking
**Objective**: Master key-value structures and learn to reach for them instinctively

**Learning (2hrs)**
- Python: `dict` creation, access, iteration, `.get()`, `.items()`, `.setdefault()`
- JS: Objects as maps, `Map` class, when to use `Map` vs plain object
- Hash-based patterns: frequency counter, grouping, lookup table
- Why hash maps turn O(n²) problems into O(n)

**Practice (2hrs)**
- LeetCode [#1 Two Sum](https://leetcode.com/problems/two-sum/) — solve with a hash map, O(n)
- LeetCode [#242 Valid Anagram](https://leetcode.com/problems/valid-anagram/)
- LeetCode [#49 Group Anagrams](https://leetcode.com/problems/group-anagrams/)
- Write a frequency counter that finds the first non-repeating character in a string

**Review (1hr)**
- Write the pattern: "When should I reach for a hash map?"

**Verification Gate**

*Coding challenge*: LeetCode [#1 Two Sum](https://leetcode.com/problems/two-sum/). Solve it in O(n) time. Walk through your solution step by step and state the time and space complexity.

*Written explanation*: Two Sum can be solved in O(n²) with a nested loop or O(n) with a hash map. Explain exactly how the hash map version works — what is stored as the key, what as the value, and why.

---

## Phase 2: Algorithms & Data Structures (Days 6–12)

---

### Day 6 — Recursion
**Objective**: Think recursively and identify base cases reliably

**Learning (2hrs)**
- Base case vs recursive case
- Call stack visualization
- When recursion is natural vs when iteration is better
- Tail recursion concept (why it matters in theory)

**Practice (2hrs)**
- Recursive factorial, Fibonacci (naive)
- LeetCode [#206 Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) — recursive version
- LeetCode [#104 Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- Write a recursive `flatten` for deeply nested arrays

**Review (1hr)**
- Trace the call stack for your Fibonacci implementation with n=5

**Verification Gate**

*Coding challenge*: Write a recursive function `power(base, exp)` that computes `base^exp` without using `**` or `Math.pow`. Then write an optimized version that runs in O(log n) by halving the exponent each call.

*Written explanation*: What is the risk of deep recursion? What is a base case and what happens if you forget one? How does the call stack relate to space complexity in recursive functions?

---

### Day 7 — Sorting Algorithms
**Objective**: Understand how major sorting algorithms work and when to use them

**Learning (2hrs)**
- Bubble sort, insertion sort, selection sort — O(n²), when they're acceptable
- Merge sort — O(n log n), divide and conquer
- Quick sort — O(n log n) average, O(n²) worst
- Built-in sort behavior in JS and Python (Timsort)

**Practice (2hrs)**
- Implement merge sort in Python
- Implement quick sort in JS
- LeetCode [#912 Sort an Array](https://leetcode.com/problems/sort-an-array/) — implement without built-ins
- LeetCode [#75 Sort Colors](https://leetcode.com/problems/sort-colors/) (Dutch national flag)

**Review (1hr)**
- Build a comparison table: algorithm, best/avg/worst time, space, stable?

**Verification Gate**

*Coding challenge*: Implement merge sort from scratch in either JS or Python. It must correctly sort `[5, 2, 8, 1, 9, 3]`.

*Written explanation*: When would you choose insertion sort over merge sort despite its worse average complexity? What does "stable sort" mean and why does it matter?

---

### Day 8 — Searching Algorithms
**Objective**: Master binary search and its variants

**Learning (2hrs)**
- Linear search: O(n), when it's the only option
- Binary search: O(log n), precondition (sorted), off-by-one pitfalls
- Binary search variants: first/last occurrence, search in rotated array
- Binary search on answer (search space, not array)

**Practice (2hrs)**
- LeetCode [#704 Binary Search](https://leetcode.com/problems/binary-search/)
- LeetCode [#34 Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
- LeetCode [#33 Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- Write binary search from memory without looking at reference

**Review (1hr)**
- Write out every off-by-one mistake you made and why

**Verification Gate**

*Coding challenge*: LeetCode [#33 Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/). Implement in O(log n).

*Written explanation*: Explain binary search in plain English — what must be true about the input, and why does it run in O(log n)? What is the most common off-by-one mistake and how do you avoid it?

---

### Day 9 — Hash Tables (Deep Dive)
**Objective**: Understand how hash tables work internally, not just how to use them

**Learning (2hrs)**
- Hash functions: what makes a good hash function
- Collision resolution: chaining vs open addressing
- Load factor and resizing
- Average O(1) vs worst-case O(n) — when does worst case happen?

**Practice (2hrs)**
- Implement a basic hash table class from scratch (with chaining) in Python
- LeetCode [#146 LRU Cache](https://leetcode.com/problems/lru-cache/)
- LeetCode [#128 Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

**Review (1hr)**
- Diagram your hash table implementation — show a collision and how chaining resolves it

**Verification Gate**

*Coding challenge*: LeetCode [#128 Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/). Solve in O(n) using a hash set. Explain why this is O(n) and not O(n²).

*Written explanation*: What is a hash collision? Describe how chaining resolves it. What is load factor and what happens when it gets too high?

---

### Day 10 — Linked Lists
**Objective**: Implement and manipulate linked lists confidently

**Learning (2hrs)**
- Singly linked list: node structure, traversal, insertion, deletion
- Doubly linked list: when and why
- Common patterns: runner technique (fast/slow pointer), dummy head node

**Practice (2hrs)**
- Implement a singly linked list class with: append, prepend, delete, print
- LeetCode [#206 Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
- LeetCode [#141 Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) (Floyd's algorithm)
- LeetCode [#21 Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

**Review (1hr)**
- Draw the pointer manipulation for reversing a 4-node list

**Verification Gate**

*Coding challenge*: LeetCode [#141 Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/). Implement using Floyd's tortoise and hare algorithm (O(1) space).

*Written explanation*: How does Floyd's cycle detection algorithm work? Why is using a `Set` to track visited nodes worse from a space complexity perspective?

---

### Day 11 — Stacks & Queues
**Objective**: Know when to use stacks and queues and implement them cleanly

**Learning (2hrs)**
- Stack: LIFO, use cases (function calls, undo, expression parsing)
- Queue: FIFO, use cases (BFS, task scheduling, print queues)
- Deque (double-ended queue)
- Monotonic stack pattern (intro)

**Practice (2hrs)**
- LeetCode [#20 Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
- LeetCode [#232 Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)
- LeetCode [#739 Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) (monotonic stack)
- Implement BFS on a graph using a queue (simple adjacency list)

**Review (1hr)**
- Trace through [#739] with input `[73,74,75,71,69,72,76,73]` step by step

**Verification Gate**

*Coding challenge*: LeetCode [#20 Valid Parentheses](https://leetcode.com/problems/valid-parentheses/). Implement from scratch.

*Written explanation*: Describe a real-world scenario where a queue is the right data structure and one where a stack is right. What is a monotonic stack and what kind of problem does it solve?

---

### Day 12 — Trees & Binary Search Trees
**Objective**: Traverse trees and understand BST properties

**Learning (2hrs)**
- Tree terminology: root, leaf, height, depth, balanced vs unbalanced
- DFS traversals: pre-order, in-order, post-order (recursive and iterative)
- BST property: left < node < right
- BST operations: insert, search, delete

**Practice (2hrs)**
- LeetCode [#104 Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- LeetCode [#226 Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
- LeetCode [#98 Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
- LeetCode [#102 Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) (BFS)

**Review (1hr)**
- Write out all three DFS traversals by hand on a sample tree

**Verification Gate**

*Coding challenge*: LeetCode [#98 Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/).

*Written explanation*: What is the time complexity of search, insert, and delete in a balanced BST vs an unbalanced one? What makes a BST degenerate into O(n) performance?

---

## Phase 3: Advanced Topics (Days 13–20)

---

### Day 13 — Heaps & Priority Queues
**Objective**: Use heaps to efficiently find mins/maxes

**Learning (2hrs)**
- Min-heap vs max-heap structure
- Heapify: building a heap in O(n)
- Insert O(log n), extract-min/max O(log n)
- Python `heapq` module; JS has no built-in (implement or use pattern)

**Practice (2hrs)**
- LeetCode [#215 Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)
- LeetCode [#703 Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)
- LeetCode [#347 Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

**Review (1hr)**
- Trace a heap insert and extract-min on a 7-element heap

**Verification Gate**

*Coding challenge*: LeetCode [#215 Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/). Solve using a min-heap of size k.

*Written explanation*: Why is a min-heap of size k the right tool for finding the kth largest element? What is the time complexity of this approach vs sorting the full array?

---

### Day 14 — Graphs: Representation & Traversal
**Objective**: Represent graphs and traverse them with BFS and DFS

**Learning (2hrs)**
- Adjacency matrix vs adjacency list — tradeoffs
- Directed vs undirected, weighted vs unweighted
- BFS: level-by-level, shortest path in unweighted graphs
- DFS: depth-first, backtracking

**Practice (2hrs)**
- LeetCode [#200 Number of Islands](https://leetcode.com/problems/number-of-islands/) (DFS)
- LeetCode [#133 Clone Graph](https://leetcode.com/problems/clone-graph/)
- LeetCode [#127 Word Ladder](https://leetcode.com/problems/word-ladder/) (BFS shortest path)

**Review (1hr)**
- Draw the BFS and DFS traversal order on the same 6-node graph

**Verification Gate**

*Coding challenge*: LeetCode [#200 Number of Islands](https://leetcode.com/problems/number-of-islands/). Implement using DFS.

*Written explanation*: When do you choose BFS over DFS on a graph? Describe what "shortest path in an unweighted graph" means and why BFS guarantees it.

---

### Day 15 — Graph Algorithms
**Objective**: Implement and understand essential graph algorithms

**Learning (2hrs)**
- Dijkstra's algorithm: shortest path in weighted graph, min-heap implementation
- Topological sort: DFS-based and Kahn's (BFS-based)
- Union-Find (Disjoint Set): structure, path compression, union by rank

**Practice (2hrs)**
- LeetCode [#743 Network Delay Time](https://leetcode.com/problems/network-delay-time/) (Dijkstra's)
- LeetCode [#207 Course Schedule](https://leetcode.com/problems/course-schedule/) (topological sort / cycle detection)
- LeetCode [#684 Redundant Connection](https://leetcode.com/problems/redundant-connection/) (Union-Find)

**Review (1hr)**
- Trace Dijkstra's on a 4-node weighted graph

**Verification Gate**

*Coding challenge*: LeetCode [#207 Course Schedule](https://leetcode.com/problems/course-schedule/). Implement using topological sort.

*Written explanation*: What is topological sort and when can it be applied (what must be true of the graph)? Describe one real-world use case.

---

### Day 16 — Dynamic Programming
**Objective**: Recognize DP problems and apply memoization/tabulation

**Learning (2hrs)**
- Two properties: overlapping subproblems + optimal substructure
- Top-down (memoization) vs bottom-up (tabulation)
- Identifying state: what changes between subproblems
- Common patterns: 1D DP (linear), 2D DP (grid/string)

**Practice (2hrs)**
- LeetCode [#70 Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
- LeetCode [#322 Coin Change](https://leetcode.com/problems/coin-change/)
- LeetCode [#300 Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
- LeetCode [#416 Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

**Review (1hr)**
- For each problem: write the recurrence relation before coding

**Verification Gate**

*Coding challenge*: LeetCode [#322 Coin Change](https://leetcode.com/problems/coin-change/). Implement bottom-up DP.

*Written explanation*: What makes a problem a DP problem? Describe what "overlapping subproblems" means using the Fibonacci sequence as an example. What is the difference between memoization and tabulation?

---

### Day 17 — Strings & Pattern Matching
**Objective**: Master string manipulation and common string patterns

**Learning (2hrs)**
- String immutability in JS and Python — performance implications
- StringBuilder pattern: why repeated concatenation is O(n²)
- Sliding window on strings
- Two-pointer on strings
- Anagram/palindrome patterns

**Practice (2hrs)**
- LeetCode [#3 Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- LeetCode [#76 Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- LeetCode [#5 Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
- LeetCode [#424 Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

**Review (1hr)**
- Write the sliding window template in both JS and Python

**Verification Gate**

*Coding challenge*: LeetCode [#3 Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/). Solve in O(n).

*Written explanation*: Why is repeated string concatenation in a loop O(n²) instead of O(n)? How does using an array/list of characters and joining at the end fix this?

---

### Day 18 — Bit Manipulation
**Objective**: Understand bitwise operations and apply common tricks

**Learning (2hrs)**
- AND, OR, XOR, NOT, left shift, right shift
- Common tricks: check if bit is set, set a bit, clear a bit, toggle a bit
- XOR trick: n ^ n = 0, n ^ 0 = n
- Powers of 2: `n & (n-1)` removes the lowest set bit

**Practice (2hrs)**
- LeetCode [#136 Single Number](https://leetcode.com/problems/single-number/) (XOR)
- LeetCode [#191 Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)
- LeetCode [#338 Counting Bits](https://leetcode.com/problems/counting-bits/)
- LeetCode [#371 Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/) (no + operator)

**Review (1hr)**
- Write out each bit operation with a concrete binary example (8-bit numbers)

**Verification Gate**

*Coding challenge*: LeetCode [#136 Single Number](https://leetcode.com/problems/single-number/). Solve using XOR only.

*Written explanation*: Explain why XOR works for the Single Number problem. Walk through the XOR operations for the array `[4, 1, 2, 1, 2]` step by step.

---

### Day 19 — OOP Principles
**Objective**: Apply OOP design and understand SOLID principles

**Learning (2hrs)**
- Encapsulation, inheritance, polymorphism, abstraction
- SOLID principles: Single Responsibility, Open/Closed, Liskov, Interface Segregation, Dependency Inversion
- Class vs prototype-based inheritance (JS)
- Abstract classes and interfaces (Python ABCs)

**Practice (2hrs)**
- Implement a shapes hierarchy: `Shape` base → `Circle`, `Rectangle`, `Triangle` with `area()` and `perimeter()`
- Implement a `Logger` class that follows Single Responsibility (one class per concern)
- Refactor a god-class example into properly separated responsibilities

**Review (1hr)**
- Write one sentence per SOLID principle with a concrete code example

**Verification Gate**

*Coding challenge*: Design a `BankAccount` class in JS or Python with: `deposit()`, `withdraw()` (throws if insufficient funds), `getBalance()`. Subclass it into `SavingsAccount` that earns 2% interest with an `applyInterest()` method. Demonstrate polymorphism.

*Written explanation*: What is the Liskov Substitution Principle? Give an example of code that violates it and explain why that creates a problem.

---

### Day 20 — System Design Basics
**Objective**: Understand the vocabulary and core trade-offs of system design

**Learning (2hrs)**
- Scalability: vertical vs horizontal scaling
- Latency vs throughput
- Caching: cache-aside, write-through, CDN
- Load balancing: round-robin, consistent hashing
- CAP theorem: consistency, availability, partition tolerance — pick two
- Database basics: SQL vs NoSQL, when to use each

**Practice (2hrs)**
- Design a URL shortener: define components, API, database schema, scale considerations
- Design a rate limiter: algorithm choices (token bucket, fixed window, sliding window)
- Write up trade-offs for each design in bullet points

**Review (1hr)**
- Draw the architecture diagram for your URL shortener

**Verification Gate**

*Coding challenge*: Implement a basic in-memory rate limiter in Python or JS. It should allow max N requests per second per user ID. Use the sliding window approach.

*Written explanation*: Explain the CAP theorem. Give a real database (e.g. PostgreSQL, Cassandra, DynamoDB) as an example of each trade-off pair and justify why.

---

## Phase 4: Web Development (Days 21–25)

---

### Day 21 — HTML5 & Accessibility
**Objective**: Write semantic, accessible HTML

**Learning (2hrs)**
- Semantic elements: `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`
- Forms: input types, `label`, validation attributes, `fieldset`
- ARIA roles and attributes: `aria-label`, `aria-describedby`, `role`
- Accessibility tree, tab order, focus management

**Practice (2hrs)**
- Build an accessible contact form with: name, email, message, submit
  - Use correct label associations
  - Add HTML5 validation (required, type, minlength)
  - Add ARIA attributes for custom error messages
- Mark up a blog post using semantic HTML (no `div` soup)

**Review (1hr)**
- Run your form through the browser's accessibility inspector

**Verification Gate**

*Coding challenge*: Write a semantic HTML page for a product listing. Include: a nav with 3 links, a main section with 3 product cards (image, name, price, "Add to cart" button), and a footer. No `div` used where a semantic element fits.

*Written explanation*: What is the difference between `aria-label` and `aria-describedby`? Why does semantic HTML improve accessibility even without ARIA?

---

### Day 22 — CSS3 Layouts: Flexbox & Grid
**Objective**: Build any layout using Flexbox and Grid confidently

**Learning (2hrs)**
- Flexbox: `flex-direction`, `justify-content`, `align-items`, `flex-wrap`, `flex-grow/shrink/basis`
- CSS Grid: `grid-template-columns/rows`, `grid-area`, `gap`, `fr` unit, `auto-fit`/`auto-fill`
- Responsive design: `@media` queries, mobile-first approach
- When to use Flexbox (1D) vs Grid (2D)

**Practice (2hrs)**
- Build a responsive 3-column card layout that collapses to 1 column on mobile (Grid)
- Build a navbar with logo left, links right, centered on mobile (Flexbox)
- Recreate a holy grail layout: header, footer, 3-column middle (Grid)

**Review (1hr)**
- Without looking at docs: write the CSS for centering a div both horizontally and vertically using Flexbox

**Verification Gate**

*Coding challenge*: Build a responsive photo gallery using CSS Grid. 4 columns on desktop, 2 on tablet, 1 on mobile. Each card has an image placeholder, a title, and a description. No JS, pure CSS.

*Written explanation*: When would you choose CSS Grid over Flexbox for a layout? Give a concrete layout example for each.

---

### Day 23 — JavaScript Deep Dive
**Objective**: Understand JS internals that trip up senior engineers

**Learning (2hrs)**
- Closures: practical use cases (module pattern, factory functions, memoization)
- Prototypal inheritance: `prototype`, `__proto__`, `Object.create()`
- Event loop: call stack, web APIs, callback queue, microtask queue
- Promises, async/await, error handling
- `this` binding: implicit, explicit (`call`/`apply`/`bind`), arrow functions

**Practice (2hrs)**
- Implement a memoize utility function using closures
- Predict and explain the output of 5 event loop puzzles (mix of setTimeout, Promises)
- Implement `Promise.all` from scratch
- Write a module using the revealing module pattern

**Review (1hr)**
- Draw the event loop with call stack, task queue, and microtask queue on a specific code snippet

**Verification Gate**

*Coding challenge*: Implement `memoize(fn)` — a function that takes any function and returns a memoized version that caches results based on arguments.

*Written explanation*: What is the difference between the microtask queue and the macrotask queue in the JS event loop? Given `setTimeout(fn, 0)` and `Promise.resolve().then(fn)`, which runs first and why?

---

### Day 24 — React Fundamentals
**Objective**: Build React UIs with hooks confidently

**Learning (2hrs)**
- JSX and how it compiles
- Component model: functional components, props, composition
- `useState`: state updates, batching, stale closures
- `useEffect`: dependencies array, cleanup, common mistakes
- Virtual DOM and reconciliation
- Controlled vs uncontrolled components

**Practice (2hrs)**
- Build a todo app: add, complete, delete todos using `useState`
- Add a filter (All / Active / Completed) using derived state (no extra state variable)
- Add a `useEffect` that saves todos to `localStorage` and loads on mount
- Build a custom hook `useLocalStorage(key, initialValue)`

**Review (1hr)**
- Explain to yourself why each `useEffect` in your app has the dependency array it does

**Verification Gate**

*Coding challenge*: Build a search-filtered list in React. It fetches a list of 20 names (you can hardcode them) and filters in real-time as the user types. Use `useState` and a controlled input.

*Written explanation*: What happens when you omit a dependency from a `useEffect` dependency array? Describe a specific stale closure bug this causes and how to fix it.

---

### Day 25 — Node.js & REST API Design
**Objective**: Build a working REST API with Express

**Learning (2hrs)**
- Node.js event loop vs browser event loop
- Express: `app`, middleware, routing, error handling
- REST principles: resources, HTTP verbs, status codes, idempotency
- Request/response lifecycle
- Middleware pattern: logging, auth, validation

**Practice (2hrs)**
- Build a REST API for a `tasks` resource:
  - `GET /tasks` — list all
  - `POST /tasks` — create
  - `GET /tasks/:id` — get one
  - `PUT /tasks/:id` — update
  - `DELETE /tasks/:id` — delete
- Add a logging middleware that logs method + path + response time
- Add basic input validation middleware for `POST /tasks`

**Review (1hr)**
- Test every endpoint with curl or Postman

**Verification Gate**

*Coding challenge*: Add authentication middleware to your tasks API. Every route requires a Bearer token in the `Authorization` header. If missing or wrong, return 401. If valid, attach a `user` object to `req` and proceed.

*Written explanation*: What is middleware in Express? Explain the `(req, res, next)` pattern. What happens if you forget to call `next()` in a middleware?

---

## Phase 5: Practice & Integration (Days 26–30)

---

### Day 26 — Algorithm Practice: Arrays, Strings, Hash Maps
**Objective**: Solve medium problems fluently

**Approach**: For each problem, before coding write: (1) approach in English, (2) time/space complexity, (3) edge cases

**Problems**
- LeetCode [#15 3Sum](https://leetcode.com/problems/3sum/) (two-pointer)
- LeetCode [#11 Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- LeetCode [#238 Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
- LeetCode [#560 Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
- LeetCode [#567 Permutation in String](https://leetcode.com/problems/permutation-in-string/) (sliding window)

**Verification Gate**

*Coding challenge*: LeetCode [#238 Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/). Solve without using division, in O(n) time.

*Written explanation*: Walk through your approach to [#238] before you see the solution. What prefix/suffix pattern did you identify?

---

### Day 27 — Algorithm Practice: Trees & Graphs
**Objective**: Pattern-match tree and graph problems quickly

**Problems**
- LeetCode [#236 Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
- LeetCode [#297 Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
- LeetCode [#210 Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) (topological sort)
- LeetCode [#417 Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)

**Verification Gate**

*Coding challenge*: LeetCode [#236 Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/).

*Written explanation*: Describe the recursive intuition behind finding the LCA — what does each recursive call return and why?

---

### Day 28 — System Design Practice
**Objective**: Think through scalable systems end-to-end

**Practice**
- Design a Twitter-like feed system:
  - Define user stories (post, follow, view feed)
  - Choose data stores (why)
  - Define API endpoints
  - Address scale: 10M users, 100M tweets/day
  - Identify bottlenecks
- Design a notification system (push, email, SMS)

**Verification Gate**

*Coding challenge*: Implement an in-memory message queue in Python or JS. It supports `publish(topic, message)`, `subscribe(topic, callback)`, and `unsubscribe(topic, callback)`. Subscribers are called when a message is published to their topic.

*Written explanation*: In your Twitter design, if a celebrity has 10M followers and posts a tweet, how do you handle fan-out? Describe push model vs pull model and the trade-offs.

---

### Day 29 — Full-Stack Project
**Objective**: Ship a complete CRUD application

**Build**: Task Manager App
- **Backend** (Node.js/Express): CRUD API for tasks with auth middleware
- **Frontend** (React): list, add, edit, complete, delete tasks
- **Integration**: React fetches from your Express API
- **Persistence**: in-memory or `localStorage` (no database required)

**Verification Gate**

*Coding challenge*: Add optimistic UI updates to your React frontend — when a task is marked complete, update the UI immediately without waiting for the API response, then rollback if the request fails.

*Written explanation*: Explain the data flow in your app from user clicking "Add Task" to the task appearing in the list. Name every step: event handler → state → API call → response → re-render.

---

### Day 30 — Mock Interview & Gap Analysis
**Objective**: Simulate a real FAANG interview and identify remaining gaps

**Session 1 (2hrs) — Mock interview**
- 45 min: two coding problems under time pressure (no hints, no searching)
  - Pick randomly from your weakest problem tags
- 45 min: system design question
- 30 min: score yourself honestly

**Session 2 (2hrs) — Gap analysis**
- Review every verification gate you failed over 30 days
- List topics you still feel uncertain about
- Write a prioritized next-30-day plan based on actual gaps

**Session 3 (1hr) — Behavioral prep**
- Write STAR answers for: biggest challenge, disagreement with a teammate, a project you're proud of

**Verification Gate**

*Coding challenge*: Solve LeetCode [#23 Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) within 30 minutes.

*Written explanation*: Rate yourself 1–10 on each phase topic. Identify your three weakest areas. For each, write what specifically you don't understand and what you'll do in the next 30 days to fix it.

---

## Daily Adjustment Log
> Updated after each day's verification gate

| Day | Topic | Gate Result | Carry-Over |
|-----|-------|-------------|------------|
| 1 | Variables & Scoping | ❌ Fail | Review var/let/const scoping, closures, and Python reference behavior |
| 2 | Control Flow & Functions | ❌ Fail | Review closures, nonlocal, function expressions, and practical implementation |
| 3 | Big O + Arrays (preview) | — | Carry-over: JS scoping exercises + Python reference exercises |
| 4 | Arrays & Lists | — | — |
| 5 | Hash Maps | — | — |
| 6 | Recursion | — | — |
| 7 | Sorting | — | — |
| 8 | Searching | — | — |
| 9 | Hash Tables | — | — |
| 10 | Linked Lists | — | — |
| 11 | Stacks & Queues | — | — |
| 12 | Trees & BST | — | — |
| 13 | Heaps | — | — |
| 14 | Graph Traversal | — | — |
| 15 | Graph Algorithms | — | — |
| 16 | Dynamic Programming | — | — |
| 17 | Strings | — | — |
| 18 | Bit Manipulation | — | — |
| 19 | OOP | — | — |
| 20 | System Design Basics | — | — |
| 21 | HTML5 | — | — |
| 22 | CSS Layouts | — | — |
| 23 | JS Deep Dive | — | — |
| 24 | React | — | — |
| 25 | Node.js & REST | — | — |
| 26 | Practice: Arrays/Strings | — | — |
| 27 | Practice: Trees/Graphs | — | — |
| 28 | System Design Practice | — | — |
| 29 | Full-Stack Project | — | — |
| 30 | Mock Interview | — | — |

---

*Report your verification gate results at the end of each day. The next day's plan will be adjusted based on what you got right or wrong.*
