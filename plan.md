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

### Day 11 — Stacks & Queues ⚠️ ADAPTED
**Objective**: Implement stacks and queues from scratch and verbalise how they work

> **Candidate context:** You can identify bugs in stack/queue code (march-24 Q10/Q12 scored well) but have a documented pattern of skipping implementation questions under pressure (march-15 Q9 blank, march-14 Q4 empty). This day has a mandatory implementation-first rule: write the code before reading the explanation.

**Learning (2hrs)**
- Stack: LIFO, use cases (function calls, undo, bracket matching)
- Queue: FIFO, use cases (BFS, task scheduling)
- Deque (double-ended queue)
- **Critical focus — `peek()` implementation**: you called `stk.peek()` in march-15 Q10 — arrays have no `.peek()` method. The correct pattern is `arr[arr.length - 1]`
- Monotonic stack pattern: what problem it solves and why

**Practice (2hrs) — implementation-first rule applies**
For each problem below: write your solution first, then run it. Do not look up syntax mid-solve.
- Write a `Stack` class from scratch (push, pop, peek, isEmpty) — no `.peek()` shortcut
- Write a `Queue` class from scratch using two stacks — understand the amortised O(1) trick
- LeetCode [#20 Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) — implement from scratch
- LeetCode [#739 Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) (monotonic stack)

**Review (1hr)**
- Trace [#739] with `[73,74,75,71,69,72,76,73]` step by step — write out the stack state after every element
- Write a 3-sentence explanation of the monotonic stack pattern in your own words, then check it against a reference

**Verification Gate**

*Coding challenge*: LeetCode [#232 Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/). Implement both `push` and `pop` — explain why `pop` is amortised O(1) not O(n).

*Written explanation (mandatory — do not skip)*: You wrote `stk.peek()` in a previous test. Explain what that returns, why it fails, and what the correct implementation is. Then describe a real-world scenario where a stack is the right data structure and one where a queue is right.

---

### Day 12 — Trees & Binary Search Trees ⚠️ ADAPTED
**Objective**: Traverse trees confidently and articulate BST properties out loud

> **Candidate context:** Recursion understanding is solid (march-24 Q1 fix was recursive and correct). The gap is translating understanding into written explanation — tree traversal requires both. This day enforces the "explain before you code" habit.

**Learning (2hrs)**
- Tree terminology: root, leaf, height, depth, balanced vs unbalanced
- DFS traversals: pre-order, in-order, post-order — write the order on paper before coding each
- BST property: left < node < right — and why in-order traversal of a BST gives a sorted sequence
- BST insert and search — trace them manually on a 5-node tree before implementing

**Practice (2hrs) — explain-first rule applies**
Before writing any code for each problem, write 2 sentences describing your approach and the expected time complexity. Then implement.
- On paper: draw a 7-node BST and write the pre-order, in-order, and post-order sequences by hand
- LeetCode [#104 Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- LeetCode [#226 Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
- LeetCode [#102 Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) (BFS — you already understand BFS queues from Day 11)

**Review (1hr)**
- Write out the three DFS traversal implementations from memory. Then explain: why does in-order traversal of a BST return values in sorted order?

**Verification Gate**

*Coding challenge*: LeetCode [#98 Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/). Before submitting, write a 2-sentence explanation of your approach.

*Written explanation (mandatory)*: What is the time complexity of search, insert, and delete in a balanced BST vs an unbalanced one? What specific insertion pattern causes a BST to degenerate into O(n) performance? Give a concrete example (e.g., inserting `[1,2,3,4,5]` in order).

---

## Phase 3: Advanced Topics (Days 13–20) — ADAPTED FOR CANDIDATE

> **Phase 3 ground rules, based on test evidence:**
> 1. **No blanks allowed.** You skipped Q6, Q7, Q8 (27 marks) in the march-24 test and Q9 in march-15. From Day 13 onward, every verification gate question must have an attempt — a partial written answer scores more than nothing.
> 2. **Explain before you implement.** Your fixes are often correct but your explanations are thin. Each practice session requires a written approach before coding.
> 3. **Complexity justification is mandatory.** Stating "O(n)" without a reason scores 50% of available complexity marks. The "why" is always required.

---

### Day 13 — Stacks & Queues: Carry-over + Heaps ⚠️ RESTRUCTURED
**Objective**: Consolidate Day 11 gaps and introduce heaps as a natural extension

> **Candidate context:** The march-24 test showed Q6 (Koko bananas — binary search on answer) and Q7 (hash table implementation) were entirely skipped. Those topics are Day 8 and Day 9 content. Before moving to heaps, the first hour of Day 13 closes those two gaps explicitly.
>
> **New March 27 checkpoint evidence:** Stack/queue implementation, BST complexity, and bounds-based BST validation are still unstable. Do not move into the full heaps workload until `MyQueue`, balanced-vs-unbalanced BST complexity, and `isValidBST` with propagated bounds are working from memory.

**Carry-over block (1hr) — mandatory, closes march-24 gaps**
- **Binary search on answer pattern** (30 min): Re-read Q6 from march-24. Implement `minEatingSpeed` from scratch. Write out the invariant: "when `canFinish` returns true, set `high = mid` not `high = mid - 1`." Understand why.
- **Hash table internals** (30 min): Re-read Q7 from march-24. Write a Python `HashTable` class from scratch with `set`, `get`, `delete`. Get Bug 1 (`append((k,v))`), Bug 2 (`hash(key)`), Bug 3 (`resize` guard) right from memory.

**Learning (1hr)**
- Min-heap vs max-heap: structure, the heap property
- Insert O(log n) — bubble up. Extract-min O(log n) — bubble down
- Python `heapq` module: `heappush`, `heappop`, negation trick for max-heap
- The pattern: "top K" problems → min-heap of size K

**Practice (2hrs)**
- On paper: insert `[5, 3, 8, 1, 4]` into a min-heap one by one, drawing the tree after each insert
- LeetCode [#215 Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) — min-heap of size k
- LeetCode [#347 Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) — bucket sort O(n) approach (you described this in march-24 Q3 but couldn't implement it — now implement it)

**Review (1hr)**
- Trace a `heappop` on a 7-element min-heap: draw the swap steps
- Write the "top K" pattern template from memory

**Verification Gate**

*Coding challenge*: LeetCode [#703 Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/). Before coding, write your approach in 2 sentences including why a min-heap of size k works here.

*Written explanation (mandatory)*: Why does a min-heap of size k give you the kth largest element? What is the time complexity of inserting n elements while maintaining size k, vs sorting the full array? Justify both.

---

### Day 14 — LRU Cache + Graph Representation ⚠️ RESTRUCTURED
**Objective**: Close the LRU cache gap from the march-24 test, then introduce graphs

> **Candidate context:** Q8 (LRU Cache) was entirely skipped in the march-24 test — 8 marks unearned. The LRU cache uses a `Map` (which you know) plus the `delete-then-reinsert` pattern for MRU promotion. This is a 30-minute closure before moving on to graphs. Do not skip it.

**Carry-over block (30 min) — mandatory**
- Implement a working `LRUCache` class in JavaScript from scratch. Requirements: `get(key)` moves key to MRU, `put(key, value)` on an existing key must `delete` then `set` (not just `set`). Test with the march-24 scenario: `put(1,1)`, `put(2,2)`, `put(1,10)`, `put(3,3)`, `get(1)` must return `10`.
- Write in your own words: why does `map.set(key, value)` alone fail when the key already exists?

**Learning (1.5hrs)**
- Graph representations: adjacency list vs adjacency matrix — when each is better
- Directed vs undirected, weighted vs unweighted
- BFS on a graph: level-by-level, uses a queue (you already know queues — connect the dots)
- DFS on a graph: uses recursion or an explicit stack

**Practice (2hrs)**
- Build an adjacency list from edge list `[[0,1],[0,2],[1,3],[2,3]]` and draw it
- LeetCode [#200 Number of Islands](https://leetcode.com/problems/number-of-islands/) — DFS. Write approach first.
- LeetCode [#133 Clone Graph](https://leetcode.com/problems/clone-graph/) — BFS with a visited map

**Review (1hr)**
- Draw the BFS and DFS traversal order on the same 6-node graph. Compare: which nodes get visited in what order?
- Write: when would you choose BFS over DFS? Give a concrete example.

**Verification Gate**

*Coding challenge*: LeetCode [#200 Number of Islands](https://leetcode.com/problems/number-of-islands/). Implement using DFS. State time and space complexity with justification.

*Written explanation (mandatory)*: In the LRU cache, why must `put` on an existing key use `delete` then `set`, rather than just `set`? Then: what is the difference between BFS and DFS traversal order? Which guarantees shortest path in an unweighted graph and why?

---

### Day 15 — Graph Algorithms ⚠️ ADAPTED
**Objective**: Implement topological sort and understand Dijkstra's at the conceptual level

> **Candidate context:** You understand directed graphs from Day 14. Graph algorithms are new territory. The pattern from tests shows you engage well when you can connect new content to something you already know — topological sort connects to BFS (Kahn's algorithm), and Dijkstra's connects to the heap you learned on Day 13.

**Learning (2hrs)**
- Topological sort: what it means, when it applies (DAG — directed acyclic graph), two approaches:
  - Kahn's algorithm (BFS-based, uses in-degree counts) — implement this one
  - DFS-based (conceptual understanding only)
- Cycle detection in directed graphs (prerequisite for topological sort)
- Dijkstra's algorithm: shortest path in weighted graph
  - Key idea: greedily pick the unvisited node with smallest known distance
  - Uses a min-heap (connect to Day 13 heap knowledge)
  - Conceptual trace only — implement is a stretch goal

**Practice (2hrs)**
- On paper: run Kahn's algorithm on a 5-node DAG. Write the in-degree table and trace which nodes get enqueued in what order
- LeetCode [#207 Course Schedule](https://leetcode.com/problems/course-schedule/) — cycle detection / topological sort
- LeetCode [#210 Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) — return the topological order, not just true/false
- Stretch: LeetCode [#743 Network Delay Time](https://leetcode.com/problems/network-delay-time/) (Dijkstra's) — attempt only after the above two are solid

**Review (1hr)**
- Trace Kahn's algorithm on `[#207]`'s graph manually before checking your code output
- Write: what must be true of a graph for topological sort to work? What breaks it?

**Verification Gate**

*Coding challenge*: LeetCode [#207 Course Schedule](https://leetcode.com/problems/course-schedule/). Before coding, write in 3 sentences: what data structures you'll use, why, and what the time complexity will be.

*Written explanation (mandatory)*: What is topological sort? What property must the graph have? Describe Kahn's algorithm step by step using the example `courses=4, prerequisites=[[1,0],[2,0],[3,1],[3,2]]`. What is the real-world use case?

---

### Day 16 — Dynamic Programming ⚠️ ADAPTED
**Objective**: Recognise DP problems and implement memoization — closing the memoization gap from march-13 and march-15

> **Candidate context:** Memoization was a documented failure across three tests: march-13 Q22 (incomplete), march-15 Q9 (blank). You understand the output of recursive code but struggle to implement memoization. This day treats memoization as the primary skill, not an afterthought.

**Learning (2hrs)**
- Two DP properties: overlapping subproblems + optimal substructure
- Fibonacci as the canonical example — trace the naive recursive calls, then show the repeated subproblems. Count how many times `fib(3)` is called for `fib(6)`
- Top-down memoization: add a cache object/dict, check before computing, store after
- Bottom-up tabulation: build from base cases upward, no recursion needed
- **The memoize wrapper pattern** (you need this): `function memoize(fn) { const cache = {}; return function(...args) { ... } }` — this was Q9 in march-15 which you left blank

**Practice (2hrs) — implement-first rule applies**
Start with memoization. Do not move to tabulation until the memoized version works.
- Implement `memoize(fn)` from scratch — a general wrapper that caches any function's results by arguments
- LeetCode [#70 Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) — solve with memoization first, then rewrite as tabulation
- LeetCode [#322 Coin Change](https://leetcode.com/problems/coin-change/) — bottom-up tabulation. Before coding, write the recurrence: `dp[amount] = min(dp[amount - coin] + 1)` for each coin
- LeetCode [#300 Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) — write the recurrence before coding

**Review (1hr)**
- For each problem: write the recurrence relation and base case from memory before checking
- Write the `memoize` wrapper from memory — this is the closure implementation you struggled with in march-15

**Verification Gate**

*Coding challenge*: LeetCode [#322 Coin Change](https://leetcode.com/problems/coin-change/). Implement bottom-up DP. State the recurrence relation explicitly in a comment before your code begins.

*Written explanation (mandatory)*: What makes a problem a DP problem? Show with Fibonacci specifically: how many times does naive recursion compute `fib(3)` when calling `fib(6)`? How does memoization fix this? What is the difference between memoization (top-down) and tabulation (bottom-up) — give one advantage of each.

---

### Day 17 — Strings & Pattern Matching ⚠️ ADAPTED
**Objective**: Solve sliding window and two-pointer string problems, and write complexity justifications

> **Candidate context:** You scored 77% on output prediction (march-13 Section C) — you understand what code does. The gap is implementing patterns. Sliding window is a pattern, not a concept: you learn it by writing the template, then applying it to problems, not by reading about it.

**Learning (2hrs)**
- String immutability: why repeated `str += char` in a loop is O(n²) — draw the memory allocations
- The sliding window template: `left`, `right` pointers, expand right, shrink left when condition violated
- Two-pointer on sorted structures
- Frequency map pattern for anagram/substring problems: `Map` for character counts (use `Map`, not object — you know why from Day 9 and march-24 Q3)

**Practice (2hrs) — write the template first**
Before solving each problem, write the sliding window template skeleton from memory:
```
let left = 0, maxLen = 0;
const window = new Map();
for (let right = 0; right < s.length; right++) {
  // expand: add s[right] to window
  // shrink: while (window violates constraint) { remove s[left]; left++ }
  // update result
}
```
Then apply it to:
- LeetCode [#3 Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) — sliding window
- LeetCode [#424 Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) — sliding window with frequency tracking
- LeetCode [#76 Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) — harder variant, attempt after the above two
- LeetCode [#5 Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) — expand-from-center (different pattern)

**Review (1hr)**
- Write the sliding window template from memory without looking
- Write the `memoize` wrapper again — reinforcement from Day 16

**Verification Gate**

*Coding challenge*: LeetCode [#3 Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/). Solve in O(n). Before submitting, write the time and space complexity with justification (not just the answer — justify each).

*Written explanation (mandatory)*: Why is repeated string concatenation (`result += char`) in a loop O(n²)? Draw the memory allocation to support your answer. How does using an array and joining at the end fix this? Also: why should you use `Map` instead of a plain object for the frequency count in these problems?

---

### Day 18 — Bit Manipulation + Complexity Justification Practice ⚠️ ADAPTED
**Objective**: Learn bit manipulation AND practise the verbal complexity justification habit

> **Candidate context:** You consistently state complexity results correctly (O(n), O(log n)) but without justification — the march-24 Q9 answer was "it's O(n)" without the amortised proof. FAANG interviews require the reasoning, not the label. Day 18 is deliberately lighter on new content to create space for justification practice.

**Learning (1.5hrs)**
- AND, OR, XOR, NOT, left shift, right shift — with 8-bit binary examples for each
- XOR properties: `n ^ n = 0`, `n ^ 0 = n` — memorise these
- `n & (n-1)` removes the lowest set bit — why: trace in binary
- Check if n is a power of 2: `n & (n-1) === 0`
- Bit masking: check if bit i is set, set bit i, clear bit i

**Practice (2hrs)**
- For every problem below: before coding, write what bit operation you'll use and why
- LeetCode [#136 Single Number](https://leetcode.com/problems/single-number/) — XOR
- LeetCode [#191 Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/) — `n & (n-1)` trick
- LeetCode [#338 Counting Bits](https://leetcode.com/problems/counting-bits/) — DP + bit trick
- **Complexity justification drill** (30 min): Take three problems you've already solved (pick from Days 11–17). For each, write the time and space complexity and justify it in 3 sentences minimum. No single-word answers.

**Review (1hr)**
- Write out each bit operation with a concrete 8-bit example
- Complexity drill: pick the hardest problem from this week and write a paragraph explaining why it has the complexity it does — as if explaining to an interviewer

**Verification Gate**

*Coding challenge*: LeetCode [#136 Single Number](https://leetcode.com/problems/single-number/). Solve using XOR only. Then: write out the XOR operations for `[4, 1, 2, 1, 2]` step by step in binary.

*Written explanation (mandatory — this is the primary gate)*: Explain why XOR works for the Single Number problem. Walk through `[4, 1, 2, 1, 2]` step by step in binary. Then: pick any problem from Days 11–17 and justify its time complexity in 3+ sentences without using the phrase "because it loops." The explanation must reference the actual operations being counted.

---

### Day 19 — OOP Principles ⚠️ ADAPTED
**Objective**: Implement class hierarchies correctly and connect OOP to patterns you've already seen

> **Candidate context:** You implemented a `BankAccount`-like closure in march-15 Q7 but got the `withdraw` logic inverted (`if amount >= 0` instead of `if amount > balance`). The Day 19 OOP bank account challenge is the same domain — treat it as fixing that mistake properly, now using classes instead of closures.

**Learning (2hrs)**
- Encapsulation: the class equivalent of closure-based private state
- Inheritance: `extends`, `super()`, method overriding
- Polymorphism: the same method name, different behaviour per subclass
- `instanceof`, `typeof` with classes
- **Connect to what you know**: the `BankAccount` closure from march-15 Q7 → now rewrite it as a class. Same logic, different syntax.
- SOLID: Single Responsibility and Liskov Substitution — the two most tested in interviews

**Practice (2hrs) — fix-it-first rule**
Start by fixing your march-15 Q7 `withdraw` bug as a class:
- Write `BankAccount` as a class with correct `withdraw` (guard: `if (amount > this.balance) throw new Error(...)`)
- Subclass into `SavingsAccount` with `applyInterest()` that adds 2% to balance
- Implement a shapes hierarchy: `Shape` (abstract) → `Circle`, `Rectangle` each with `area()` and `perimeter()`
- Write a `Logger` class that logs to console — then explain: what Single Responsibility means for it

**Review (1hr)**
- Write from memory: what is Liskov Substitution? Write one example that violates it
- Trace: if `SavingsAccount extends BankAccount`, and you call `account.withdraw(50)` on a `SavingsAccount` instance — which method runs?

**Verification Gate**

*Coding challenge*: Implement `BankAccount` and `SavingsAccount` as described. The `withdraw` method must throw (not return an error string) when funds are insufficient. `applyInterest()` must actually update `this.balance`. Demonstrate both with test calls.

*Written explanation (mandatory)*: What is the Liskov Substitution Principle? Write a concrete example in JS or Python that violates it and explain what breaks at runtime. Then: what is the difference between using a closure for private state (your march-15 Q7 approach) vs using a class? When would you choose each?

---

### Day 20 — System Design + Refactoring + Design Patterns Deviation ✅ COMPLETED
**Date completed:** April 3, 2026
**Result:** 37/100 — focus session triggered (`tests/april-3/`)
**Focus gate:** In progress — `tests/april-3-2nd/` (38/50 required to advance)

**What was assessed:**
- System design vocabulary (CAP, caching, scalability, SQL vs NoSQL) — strongest section (65%)
- Refactoring catalog: smell identification reliable (75%), technique naming consistently wrong
- Design pattern classification: category recognition partial, participant roles skipped
- Pattern implementation (Factory Method, Observer, Decorator): entirely blank — 25 marks lost
- Rate limiter: approach correct, implementation broken in 5 places

**Carry-over into Day 21:**
- Must name technique (not smell) when asked for the refactoring action
- Must write Factory Method, Observer, Decorator from a blank page
- Rate limiter: understand and fix all 5 bugs from the original submission

---

### Day 21 — Design Patterns: Consolidation Gate + Strategy + Adapter ⚠️ GATED
**Prerequisite:** Pass focus gate (`tests/april-3-2nd/`) at 38/50 before starting this day.
If the gate is failed: spend 30 min on the one weakest pattern from the gate, then advance regardless — do not stay blocked here another full day.

**Objective:** Lock in Factory Method, Observer, and Decorator through fresh scenarios. Add Strategy and Adapter.

> **Candidate context:** The focus session gave you the exact code shapes. Day 21 uses different scenarios for all three patterns — same shape, different context. If the pattern only works on the drill example, it has not transferred. The ratio today is 20 min reading, 2.5 hrs writing.

**Verbal check (15 min) — mandatory before anything else**
Write from memory, no notes:
1. Name the three participants in the Observer pattern.
2. Name the three participants in the Factory Method pattern.
3. Name the three participants in the Decorator pattern.
If you cannot answer these, read for 10 minutes, then answer from memory. Do not start drills until you can.

**Learning (30 min) — two new patterns only**

*Strategy Pattern*
- Intent: define a family of algorithms, put each in its own class, make them interchangeable at runtime
- Participants: Context (holds a strategy reference and delegates to it), Strategy (the interface), ConcreteStrategy (one specific implementation)
- When to use: multiple ways to do the same operation (sort algorithms, shipping cost calculators, payment methods) and you need to switch without if/else

*Adapter Pattern*
- Intent: convert the interface of a class into the interface a client expects — a wrapper that translates
- Participants: Target (the interface the client wants), Adaptee (the existing class with the wrong interface), Adapter (wraps Adaptee, implements Target)
- When to use: integrating a third-party library or legacy class that does not fit your interface

**Implementation drills (2.5 hrs)**

Before each drill: write the class signatures (constructor + method names only), then fill in the bodies. This prevents the blank-page freeze.

*Drill 1 — Strategy (45 min)*
Build a `Sorter` class that can sort an array using interchangeable strategies. Create two concrete strategies: `BubbleSortStrategy` and `QuickSortStrategy`. The `Sorter.sort(array)` method delegates entirely to whichever strategy is currently set. The client code should be able to swap strategies at runtime without modifying `Sorter`.

Before coding: write the algorithm in 2 sentences — what does the Context hold and what does it call?

*Drill 2 — Adapter (45 min)*
You have a `LegacyLogger` class with a method `writeLog(message, level)`. Your new system expects all loggers to implement `log({ message, severity })`. Write an `Adapter` that wraps `LegacyLogger` and implements the new interface.

Before coding: identify which is the Target, which is the Adaptee, and what the Adapter must translate.

*Drill 3 — Fresh Observer (30 min)*
Write a `NewsPublisher` that notifies subscribers whenever a new article is published. Two concrete observers: `EmailSubscriber` (logs `[Email] New article: {title}`) and `AppNotification` (logs `[App] Breaking: {title}`). The publisher must support `subscribe`, `unsubscribe`, and `publish(title)`.

*Drill 4 — Fresh Factory Method (30 min)*
Write a `CompressionFactory` with three strategies: `ZipCompressor`, `GzipCompressor`, `BrotliCompressor`. Each has a `compress(data)` method. Client code should only call `CompressionFactory.create(type)` — never `new ZipCompressor()` directly.

**Verification Gate**

*Coding challenge*: Write a `Router` class using the Strategy pattern. It holds a routing strategy and a `findRoute(start, end)` method that delegates to it. Create two concrete strategies: `FastestRoute` (logs `"Taking fastest route from X to Y"`) and `ScenicRoute` (logs `"Taking scenic route from X to Y"`). Show the router switching strategies at runtime without modifying the `Router` class.

*Written explanation*: What is the difference between the Strategy pattern and the Factory Method pattern? They both involve swapping implementations — name the one key distinction. Give one real scenario where Strategy is clearly the better choice and one where Factory Method is clearly the better choice.

---

### Day 22 — Web Fundamentals I: HTML5 + CSS3 (Compressed)
**Objective:** Write semantic, accessible HTML and build real layouts with Flexbox and Grid.

> **Candidate context:** HTML and CSS are less algorithmically demanding than everything you have done in the last 21 days. The goal is working, semantic output — not memorising every property. Move at pace. If a section feels obvious, test yourself and move on. The verbal check here matters because the most common mistake is using `div` for everything.

**Verbal check (10 min)**
Write from memory:
1. Name 5 semantic HTML elements and the non-semantic `<div>` they replace.
2. What is the difference between `justify-content` and `align-items` in Flexbox?
3. When would you use CSS Grid over Flexbox?

**Learning (1 hr)**

*HTML5 (30 min)*
- Semantic elements: `header`, `nav`, `main`, `section`, `article`, `aside`, `footer` — one use case each
- Forms: `label` + `input` associated by `for`/`id`, HTML5 validation (`required`, `type`, `minlength`, `pattern`)
- ARIA: `aria-label`, `aria-describedby`, `role` — when each applies and when semantic HTML makes them unnecessary
- Accessibility tree, tab order, focus management

*CSS3 (30 min)*
- Flexbox: `flex-direction`, `justify-content`, `align-items`, `flex-wrap`, `flex-grow`, `flex-shrink`
- Grid: `grid-template-columns`, `gap`, `fr` unit, `auto-fit` + `minmax`, `grid-area`
- Responsive: `@media` queries, mobile-first approach
- When to reach for Flexbox (1D layout) vs Grid (2D layout)

**Implementation drills (2.5 hrs)**

*Build 1 (1 hr): Accessible contact form*
- Fields: name, email, message, submit
- Every input has a `<label>` correctly associated by `for`/`id`
- HTML5 validation: `required`, `type="email"`, `minlength="10"` on message
- One ARIA attribute used correctly (your choice — justify it in a comment)
- No `<div>` wrapping labels that a `<fieldset>` should handle

*Build 2 (1 hr): Responsive 3-column card grid*
- Desktop: 3 equal columns
- Tablet (≤768px): 2 columns
- Mobile (≤480px): 1 column
- Use CSS Grid with `auto-fit` and `minmax` — not three separate media queries
- Each card: image placeholder, name, price, button

*Build 3 (30 min): Flexbox navigation bar*
- Logo on the left, 4 links on the right
- Links spread evenly using Flexbox
- On mobile (≤600px): links stack vertically

**Verification Gate**

*Coding challenge*: Build a semantic product listing page from scratch. Must include: a `<nav>` with 3 links, a `<main>` with 3 product cards laid out in a CSS Grid (responsive), and a `<footer>` with a copyright line. No `<div>` where a semantic element fits. All interactive elements are keyboard accessible.

*Written explanation*: What is the difference between `aria-label` and `aria-describedby`? Give a concrete example of when you would use each. Why does semantic HTML improve accessibility even without any ARIA attributes?

---

### Day 23 — JavaScript in the Browser: DOM, Events, Fetch, Async/Await
**Objective:** Manipulate the DOM, handle events correctly, and use Fetch with async/await.

> **Candidate context:** This day reconnects your JavaScript foundations to the browser. The event loop knowledge from Day 3 applies directly to async/await. The closure knowledge from Day 2 applies to event handler scope. Do not skip the verbal check — the event loop and closure gaps from the early weeks are exactly what this day tests.

**Verbal check (15 min) — mandatory**
Write from memory:
1. What is the event loop? Why does `setTimeout(fn, 0)` not always run immediately after the current line?
2. What is the difference between a Promise and async/await? Are they different technologies or the same?
3. What does `event.preventDefault()` do and name one situation where you need it?
4. In a closure created inside a `for` loop, what value does the closed-over variable hold if you use `var`? Why?

**Learning (1 hr)**
- DOM: `querySelector`, `querySelectorAll`, `createElement`, `appendChild`, `remove()`, `innerHTML` vs `textContent` (and why `innerHTML` is risky)
- Events: `addEventListener`, event bubbling, event delegation, `event.target` vs `event.currentTarget`
- Promises: the `.then()` / `.catch()` / `.finally()` chain
- Fetch API: `fetch(url)` → `.json()`, error handling (why a 404 does NOT reject the Promise)
- `async/await`: syntax sugar over Promises, `try/catch` for errors, `await Promise.all([...])` for parallel
- Why callback hell → Promises → async/await was a progression in the language

**Implementation drills (2 hrs)**

*Drill 1 (45 min): Live search filter*
- Render a hardcoded list of 10 items from a JS array into the DOM
- An `<input>` at the top that filters the list live as the user types (no page reload)
- The filter is case-insensitive
- After: explain in a comment why you did NOT attach one listener per list item

*Drill 2 (45 min): Fetch + render*
- Fetch from `https://jsonplaceholder.typicode.com/users` on page load
- Render each user's name and email as a card
- Show a "Loading..." state while the fetch is in progress
- Show an error message if the fetch fails — do NOT let the app crash silently
- Use async/await, not `.then()` chains

*Drill 3 (30 min): Event delegation*
- A `<ul>` with dynamically added list items, each containing a "Delete" button
- Use a single `addEventListener` on the `<ul>`, not one per button
- Write a comment explaining how `event.target` lets you identify which button was clicked

**Verification Gate**

*Coding challenge*: Build a comment section. A `<textarea>` and a "Post" button. On click: add the comment as a `<li>` to a `<ul>`, clear the textarea, and prevent default form submission. Each `<li>` has a "Delete" button that removes only that item. Use event delegation for all delete buttons — one listener total on the `<ul>`.

*Written explanation*: What is the difference between `event.target` and `event.currentTarget`? Trace through your event delegation solution and explain which one you used and why the other would not work.

---

### Day 24 — React Fundamentals
**Objective:** Build interactive UIs with components, state, props, and useEffect.

> **Candidate context:** React is a shift in mental model — the UI is a function of state, not a sequence of DOM mutations. When state changes, React re-renders the component. Think of each component as a pure function: same props and state in, same output. Build first, read second — the mental model clicks through building, not through reading.

**Verbal check (10 min)**
Write from memory (if you cannot answer these, read for 10 minutes then answer — do not start drills until you can):
1. What is the difference between props and state? Which one can a component change?
2. When does `useEffect` run? What does the dependency array `[]` mean vs `[value]` vs no array at all?

**Learning (1 hr)**
- JSX and why `React.createElement` is what it compiles to
- Functional components and the component tree
- `useState`: declaration, update, why updates are asynchronous (batching)
- `useEffect`: run on mount, on update, cleanup function on unmount
- Props: passing data down, why props flow one direction
- Lifting state up: when two sibling components need the same data
- Conditional rendering: `&&` operator, ternary
- Lists and the `key` prop: why React needs it and what happens without it
- Controlled inputs: `value` from state + `onChange` handler

**Implementation drills (2.5 hrs)**

*Build 1 (1 hr): Counter with history*
- A number display, an increment button, a decrement button, a reset button
- Below the counter: a list of every value the counter has held, in order
- All state in a single component
- The history must update correctly even when reset is pressed

*Build 2 (1 hr): Fetch + React*
- `useEffect` fetches `https://jsonplaceholder.typicode.com/posts?_limit=5` on mount
- Renders posts as cards (title + body)
- A "Refresh" button that triggers a new fetch
- Three UI states handled: loading, success, error

*Build 3 (30 min): Controlled form with list*
- Name + email inputs, both controlled
- Submit adds the entry to a list displayed below
- Inputs clear after submit
- If either field is empty, show an inline error and do not add the entry

**Verification Gate**

*Coding challenge*: Build a Todo app. Requirements: add a task via a controlled input + button, mark a task complete (toggle line-through style), delete a task, show a count of incomplete tasks remaining. All state in a single parent component. No external libraries or frameworks beyond React.

*Written explanation*: Explain "lifting state up." In your Todo app, why does the full task list live in the parent and not inside each individual Todo item component? What would break if each item managed its own "completed" state independently?

---

### Day 25 — Node.js + REST API with Express
**Objective:** Build a working REST API and connect it to the React frontend from Day 24.

> **Candidate context:** Node.js is JavaScript on the server. The patterns are identical — functions, modules, async/await. The new concept is the request/response cycle and middleware. Start with the shape of an Express app, then add complexity layer by layer. Do not try to understand all of Express before writing the first route.

**Verbal check (10 min)**
Write from memory:
1. What is middleware in Express? What do `req`, `res`, and `next` represent?
2. What is the difference between `GET` and `POST`? Name one situation where you must use POST rather than GET.
3. What does `res.json()` do that `res.send()` does not?

**Learning (1 hr)**
- Node.js module system: `require` / `module.exports` vs ES module `import/export`
- Express: `app.get`, `app.post`, `app.put`, `app.delete`, `app.use`
- Middleware: `express.json()` (body parsing), custom middleware, `next()` and what happens if you forget to call it
- Route parameters: `req.params`, `req.body`, `req.query`
- Error handling middleware: the four-argument form `(err, req, res, next)`
- CORS: why it exists, how the `cors` package fixes it for local development
- HTTP status codes: 200, 201, 400, 401, 404, 500 — one use case each

**Implementation drills (2 hrs)**

*Build 1 (1.5 hrs): Tasks REST API*
In-memory array as the data store (no database needed).
- `GET /tasks` — return all tasks (200)
- `POST /tasks` — create a new task (`{ title }` in body), return the created task (201)
- `PUT /tasks/:id` — update task (`{ completed }` in body), return updated task (200), 404 if not found
- `DELETE /tasks/:id` — remove task (204), 404 if not found
- A custom 404 handler for all unmatched routes
- `express.json()` middleware applied globally

*Build 2 (30 min): Connect to your Day 24 React app*
- Add `cors` middleware to the Express API
- Point the React `fetch` calls at `http://localhost:3000`
- Verify: add a task in the React UI, refresh the page — the task should still exist (it is in memory, so it will reset on server restart — that is fine for now)

**Verification Gate**

*Coding challenge*: Add a reusable auth middleware to the Tasks API. It should check for an `Authorization: Bearer secret123` header. If the header is missing or the token is wrong, respond with `{ error: "Unauthorized" }` and status 401. Apply it only to `POST`, `PUT`, and `DELETE` routes — `GET` routes stay public. Write the middleware as a standalone function, not inline.

*Written explanation*: What is middleware in Express? Explain the `(req, res, next)` pattern in your own words. What happens if a non-terminal middleware never calls `next()`? What is the difference between calling `next()` and calling `next(err)`?

---

### Day 26 — Algorithm Implementation Sprint: Carry-Over Clearance ⚠️
**Objective:** Close the active carry-overs from Days 13–17 through focused drilling, not testing.

> **Candidate context:** Topological sort, sliding window, DP, and graph BFS have been tested on four separate papers without fully transferring. This day is not a test — it is a deliberate practice session. You write each algorithm from scratch, trace it by hand, then write it again from memory in a different scenario. No score. No pass/fail. The goal is that tomorrow these feel automatic.

**Rules for this day:**
- Write the algorithm in plain English (2–3 sentences) before writing any code
- After each implementation: trace it manually with a small example
- After the trace: close your notes and write it again from scratch in a new scenario
- Complexity justification required after every implementation — the label alone is not enough

**Verbal check (15 min) — mandatory**
Write from memory before any coding:
1. Topological sort: name the two data structures it requires and why each is needed.
2. Sliding window: what is the invariant? When does a fixed window slide vs when does a variable window shrink?
3. DP climbing stairs: write the recurrence relation in one line before you write any code.
4. BFS: why does a queue give you shortest path but DFS does not?

**Drill block (3 hrs — 45 min each)**

*Drill A — Topological Sort*
Write `buildOrder(numCourses, prerequisites)` from scratch. Return a valid course order. Return `[]` if there is a cycle. Use in-degree + queue (Kahn's algorithm).

Step 1: write the algorithm in English.
Step 2: write the code.
Step 3: trace for `numCourses=4, prerequisites=[[1,0],[2,0],[3,1],[3,2]]` — write out in-degree values and the queue state after each dequeue.
Step 4: write it again from scratch in a new scenario (package build order, task scheduling — your choice).

*Drill B — Sliding Window (both types)*
Write `maxSumSubarray(nums, k)` — fixed window, return the maximum sum of any k consecutive elements.
Write `longestSubstringWithoutRepeat(s)` — variable window.

For each: state the invariant before coding. After coding: trace one example for each. State the time and space complexity with one sentence of justification.

*Drill C — Dynamic Programming*
Write `minCostClimbingStairs(cost)`. Write the recurrence first: `dp[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2])`. Then implement it.

Then write `uniquePaths(m, n)` — how many ways to travel from top-left to bottom-right of an m×n grid moving only right or down. Write the recurrence first.

*Drill D — Graph BFS*
Write BFS that returns the shortest path (as an array of node values) between a start and end node in an unweighted undirected graph. If no path exists, return `[]`.

After: explain in writing why Dijkstra would be needed if the edges had weights.

**Verification Gate**

Three fresh LeetCode-style problems. Explanation-first required — write 2–3 sentences of approach before any code:

1. [#210 Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) — topological sort
2. [#3 Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) — sliding window
3. [#746 Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/) — DP

For each: state time and space complexity with justification. No blanks — an incomplete solution with a clear explanation of what is missing scores more than silence.

---

### Day 27 — System Design Deep Dive
**Objective:** Move from system design vocabulary (Day 20) to trade-off reasoning backed by specific technology choices.

> **Candidate context:** Day 20 showed you understand the concepts but give vague answers when pressed for specifics — no database names for CAP pairs, no concrete bottleneck analysis. Day 27 fixes that. Every answer must name a real technology and justify the choice in one sentence. Vague answers ("use a cache") score zero here.

**Verbal check (15 min)**
Write from memory:
1. Name one CP database, one AP database, and one CA database. For each: what does it sacrifice and why is that acceptable in its typical use case?
2. Explain the cache-aside pattern in 3 sentences. What happens on a cache miss?
3. What is the difference between a message queue and a pub/sub system? Name a real technology for each.
4. What is database sharding? What is the hardest problem it introduces?

**Learning (1 hr) — depth on four specific concepts**
- Load balancers: round-robin vs least-connections vs consistent hashing — when consistent hashing is essential (hint: stateful services)
- Database read replicas: why they help reads, why they cannot help writes, replication lag
- Message queues vs event streaming: RabbitMQ (queue — message consumed once) vs Kafka (stream — message replayed, ordered by partition)
- CDN: what it caches (static assets, sometimes API responses), what it cannot cache (user-specific data), cache invalidation strategies

**Design sessions (2 hrs)**

*Design 1 (1 hr): URL Shortener at scale*
Write the design in this exact order — do not skip steps:
1. Functional requirements (2–3 bullet points)
2. Non-functional requirements (scale targets: reads/writes per second)
3. API design (`POST /shorten`, `GET /:code`)
4. Data model (table name, columns, why you chose SQL or NoSQL)
5. Components (load balancer, app servers, cache, database — draw as text diagram)
6. Bottleneck analysis: where does the system break first at 10M users?
7. Scaling decisions: name at least 3 concrete changes and justify each

*Design 2 (1 hr): Notification system*
Requirements: send push, email, and SMS notifications reliably. Retry on failure. Adding a new channel (e.g. Slack) must not require modifying the core dispatch logic.

In your design: name the design pattern you are using for the channel abstraction. Name the queue technology. Explain what "at-least-once delivery" means and how you handle duplicate notifications.

**Verification Gate**

*Design challenge*: Design a rate limiter as a distributed service (not in-memory). It must work correctly when deployed across 100 API servers. Name the data store and algorithm. Explain what happens if the data store goes down — does the system fail open or fail closed, and why?

*Written explanation*: What is the difference between horizontal scaling and database sharding? A read-heavy system (10:1 read/write ratio) is hitting database limits. Name two specific techniques you would apply (not "add more servers") and justify each in one sentence.

---

### Day 28 — Full-Stack Integration Project
**Objective:** Build a complete working application that connects HTML/CSS, React, Node/Express, and at least one design pattern.

> **Candidate context:** This is the first day you build something end-to-end without scaffolding or a question prompt telling you what to do. When you get stuck: write what you know, name the gap explicitly, and work around it. A partially working app you can explain is more valuable than a blank page. Commit to a scope and finish it — do not expand the scope mid-build.

**Project: Task Manager with Auth and Observer**

Build a task manager app where:

Backend (Express):
- All CRUD routes from Day 25 (`GET`, `POST`, `PUT`, `DELETE` on `/tasks`)
- Auth middleware on write routes (Bearer token)
- `GET /tasks?completed=true/false` — filter by status
- `createdAt` timestamp on every task

Frontend (React):
- Fetch all tasks on load
- Add task via controlled form
- Mark task complete / incomplete (toggle)
- Delete a task
- Filter tabs: "All", "Active", "Completed"
- Handle loading, error, and empty states
- Do not crash on API errors — show a message

Design pattern requirement:
- Use the Observer pattern in at least one place in the frontend state management or event handling
- Document in a comment: what is the Subject, what is the Observer, what event triggers notification

**Verification Gate**

Demo the working app (or walk through the code if not fully deployed). Then answer in writing:
1. Walk through the full data flow for "user clicks Add Task" — name every step from the click event to the task appearing in the list. Be specific: event handler → state update → API call → response → re-render.
2. Where did you apply the Observer pattern? What would break if you removed it?
3. Name one thing you would change if this app needed to support 10,000 concurrent users.

---

### Day 29 — Mock Interview Prep: Algorithm Problems + System Design Under Pressure
**Objective:** Simulate interview conditions. Time pressure, no hints, explanation-first. This is a rehearsal for Day 30.

> **Candidate context:** The rules change today. No looking things up mid-problem. No blanks. A broken partial solution with a clear explanation of where it breaks scores better than leaving a question unattempted. This is the one pattern from your test history that has cost the most marks — practice the habit of always writing something.

**Session 1 (1.5 hrs) — Timed algorithm problems**
20 minutes per problem. Write the approach (2–3 sentences) before any code.

Choose 3 from the set based on your weakest carry-over areas:
- [#207 Course Schedule](https://leetcode.com/problems/course-schedule/) — topological sort / cycle detection
- [#3 Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) — sliding window
- [#322 Coin Change](https://leetcode.com/problems/coin-change/) — DP
- [#200 Number of Islands](https://leetcode.com/problems/number-of-islands/) — graph BFS/DFS
- [#49 Group Anagrams](https://leetcode.com/problems/group-anagrams/) — hash map

After each: state time and space complexity with justification. No label-only answers.

**Session 2 (1 hr) — System design under time pressure**
30 min: Design a real-time collaborative document editor (like Google Docs — simplified).
- Start with: what are the two hardest technical problems?
- Propose a data model and a conflict resolution strategy (you do not need to fully solve it — name the approach)
- Name one technology you would use and why

30 min: Debrief in writing — what did you state clearly, what did you skip, what would you add with 10 more minutes?

**Session 3 (30 min) — Behavioral prep**
Write STAR answers (Situation, Task, Action, Result) for:
1. A time you had to learn something complex quickly under pressure
2. A time you made a technical mistake and how you fixed it
3. A project you are proud of and one thing you would do differently now

---

### Day 30 — Full Mock Interview + Gap Analysis + Next Plan
**Objective:** Simulate a real FAANG-format interview. Score yourself honestly. Write the next 30 days.

> **Candidate context:** This is a checkpoint, not a finish line. The most valuable output of Day 30 is not the interview score — it is the gap list. Be as specific about what broke as you would be in a post-incident review. Vague self-assessments ("I need more practice") are not acceptable here.

**Session 1 (2 hrs) — Full mock interview**
No notes. No looking up.
- 45 min: Two coding problems from your weakest LeetCode tags (use your Day 29 self-assessment to pick)
- 45 min: System design — design a distributed job scheduler (or any system design question you have not seen before)
- 30 min: Score yourself against the following rubric:
  - Did you explain your approach before coding?
  - Did you name time and space complexity with justification?
  - Did you check edge cases before submitting?
  - Did you leave any blanks?
  - Did you name specific technologies in the system design?

**Session 2 (1.5 hrs) — Gap analysis**
Review every gate result from Days 1–30. For each gate you failed or only partially passed:
- Name the topic
- Describe the specific failure mode (not "I struggled" — what exactly broke in the code or explanation?)
- Write one concrete action to fix it in the next 30 days

Produce a prioritised gap list with these three categories:
1. Algorithm patterns that need more reps (name the specific tag)
2. System design components that need deeper study (name the specific concept)
3. Design patterns or OOP concepts that still break on blank-page implementation

**Session 3 (30 min) — Next 30 days**
Write a specific plan for the next 30 days based on your gap list. Must be concrete:
- Which 3 LeetCode tags will you drill daily?
- Which 2 system design case studies will you study in depth?
- Which design patterns still need 3+ blank-page implementations before they are stable?

---

## Daily Adjustment Log
> Updated after each day's verification gate

| Day | Topic | Gate Result | Carry-Over |
|-----|-------|-------------|------------|
| 1 | Variables & Scoping | ❌ Fail (36%) | Review var/let/const scoping, closures, Python reference behavior |
| 2 | Control Flow & Functions | ❌ Fail (36%) | Review closures, nonlocal, function expressions, practical implementation |
| 3 | MAR 15 - REMEDIATION | FAILED | Focus: Hoisting, Event Loop, Closure Patterns, Type Coercion |
| 4 | Arrays & Lists | — | — |
| 5 | Hash Maps | — | — |
| 6 | Recursion | — | — |
| 7 | Sorting | — | — |
| 8 | Searching | — | — |
| 9 | Hash Tables | — | — |
| 10 | Linked Lists | ✅ Completed (march-24 test: 58/100) | Carry-over to Day 13: hash table bugs (Q7, 0/12) and LRU cache (Q8, 0/8). Complexity justification thin across all sections. |
| 11 | Stacks & Queues (ADAPTED) | ❌ Fail checkpoint, ⚠️ partial narrow recovery, then ❌ broad transfer misses on March 28 (30/100) and March 30 (40/100) fresh papers | Browser-history style state handling is still not exact; after back/visit, forward-history invariants must be drilled explicitly before widening scope. |
| 12 | Trees & BST (ADAPTED) | ⚠️ Partial, but stronger than the surrounding topics on March 30 | LCA-in-BST reasoning is now a relative strength, but tree implementation precision still needs carry-over for full transfer confidence. |
| 13 | Heaps + carry-over: binary search on answer + hash table (RESTRUCTURED) | ❌ Still not ready to open fully after March 30 cumulative review | Keep Day 13 narrow: binary-search-on-answer, hash-table / bucket thinking, and no-blanks enforcement remain active. |
| 14 | LRU Cache fix + Graph Representation (RESTRUCTURED) | ⚠️ Partial on March 30 cumulative review | Graph representation and LRU refresh logic are visible, but BFS output and queue precision need another exact fresh check. |
| 15 | Graph Algorithms (ADAPTED) | ❌ Fresh transfer miss on March 30 cumulative review | Topological sort was left blank; re-test in-degree plus queue directly before treating Day 15 as opened. |
| 16 | Dynamic Programming (ADAPTED) | ⚠️ Partial on March 30 cumulative review | Rolling-DP structure is improving, but recurrence explanation and complexity justification still need tightening. |
| 17 | Strings (ADAPTED) | ❌ Fresh transfer miss on March 30 cumulative review | Fixed-size sliding-window logic did not transfer; re-test permutation-in-string with frequency counts and exact control flow. |
| 18 | Bit Manipulation + Complexity Justification (ADAPTED) | ⚠️ Partial on March 30 cumulative review | XOR implementation was correct, but trace quality and "why it works" explanation still need to become explicit and reliable. |
| 19 | OOP (ADAPTED) | ⚠️ Partial on March 30 cumulative review | Inheritance / LSP direction is visible, but method contracts and thrown-error behavior still slip on exact implementation. |
| 20 | System Design + Verbal Review + Deviation: Refactoring & Design Patterns (ADAPTED) | ❌ Fail (37/100) | Smell identification is reliable but technique naming consistently wrong; Factory Method, Observer, Decorator implementations were blank (25 marks lost); rate limiter broken in 5 places; system design concepts solid. Focus session required before Day 21. |
| 20.5 | FOCUS SESSION: Refactoring techniques vs smells + Factory/Observer/Decorator from scratch + Rate Limiter fix | ❌ Gate not passed (23/50 — needed 38/50) | Factory Method structure transferred (major improvement from blank). Observer broken by property name mismatch + copy-paste error. Decorator fundamentally misunderstood (wrapping vs extending). Advancing to Day 21 regardless — carry-overs active: (1) Q1d Divergent Change → Extract Class, (2) property name mismatch habit, (3) Decorator wrapping concept. |
| 21 | HTML5 | — | — |
| 22 | CSS Layouts | — | — |
| 23 | JS Deep Dive | — | — |
| 24 | React | — | — |
| 25 | Node.js & REST | — | — |
| 26 | Practice: Arrays/Strings | — | — |
| 27 | Practice: Trees/Graphs | — | — |
| 28 | System Design Practice / April 12 MCQ Marathon | ⚠️ Advance with carry-over (94/120, 78.3%) | Broad system design vocabulary is solid, but carry over concrete tool matching (Kafka/RabbitMQ/Redis/Elasticsearch), cache/replica nuance, reliability concepts, and API/observability recall before treating system design as consolidated. |
| 29 | Full-Stack Project | — | — |
| 30 | Mock Interview | — | — |

---

*Report your verification gate results at the end of each day. The next day's plan will be adjusted based on what you got right or wrong.*
