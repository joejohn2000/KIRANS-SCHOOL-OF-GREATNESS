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

### Day 20 — System Design Basics + Full Verbal Review ⚠️ ADAPTED
**Objective**: Learn system design vocabulary and consolidate the verbal explanation habit built across Days 11–19

> **Candidate context:** System design is new territory. The risk given your test pattern is that you engage with the concepts but skip the verbal/written part. Day 20 reverses the ratio: 1hr of new content, 1hr of design practice, and 1hr of verbal review of the past 10 days. The verbal review is not optional.

**Learning (1hr) — core vocabulary only**
- Scalability: vertical vs horizontal scaling — one concrete difference
- Latency vs throughput — define both, give a concrete example of a trade-off
- Caching: cache-aside pattern — when does a cache miss happen and what then?
- CAP theorem: consistency, availability, partition tolerance — pick two. One real database per pair:
  - CP: HBase (consistent + partition-tolerant, sacrifices availability)
  - AP: Cassandra (available + partition-tolerant, sacrifices consistency)
  - CA: PostgreSQL (consistent + available, no partition tolerance — single node)
- SQL vs NoSQL: when each fits — 2 sentences each

**Practice (2hrs)**
- Design a URL shortener in writing: components, API (`POST /shorten`, `GET /:code`), database schema, how you'd scale it to 10M users
- Implement a sliding window rate limiter in JavaScript: `allow(userId)` returns true/false. Max 5 requests per 10 seconds per user. Use a `Map<userId, timestamps[]>`.
- Write the trade-offs for both designs as bullet points — at least 3 trade-offs per design

**Review (1hr) — mandatory verbal review of Days 11–19**
Answer each of the following in writing (2–3 sentences each). No looking up:
1. What is the difference between a stack and a queue? Give a use case for each.
2. What is the in-order traversal of a BST and why is it sorted?
3. What is the heap property? Why is heap insert O(log n)?
4. What is the LRU cache bug you fixed — why does `map.set` alone fail?
5. What is the sliding window template — write it from memory.
6. What is the `memoize` wrapper — write it from memory.
7. Pick the hardest complexity justification you did on Day 18 and repeat it.

**Verification Gate**

*Coding challenge*: Implement a sliding window rate limiter in JavaScript: `allow(userId)` — max N requests per window of W milliseconds. Prune timestamps older than W on each call. State time and space complexity with justification.

*Written explanation (mandatory)*: Explain the CAP theorem. Give a real database as an example of each pair (CP, AP, CA) and justify why it sits in that category. Then answer: in your URL shortener design, what is the bottleneck at 10M users and how would you address it?

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
| 11 | Stacks & Queues (ADAPTED) | ❌ Fail checkpoint, ⚠️ partial narrow recovery, then ❌ broad transfer miss on March 28 paper (30/100 overall) | Exact fresh implementations still break under pressure; keep stack/queue work narrow and exact before widening scope. |
| 12 | Trees & BST (ADAPTED) | ⚠️ Partial, but not transferred cleanly to fresh paper | Traversal / BST reasoning are better than before, but fresh implementation still breaks; carry over `insertIntoBST` and typo-free `isValidBST`. |
| 13 | Heaps + carry-over: binary search on answer + hash table (RESTRUCTURED) | ❌ Not ready to open fully | Do not widen to full Day 13 yet. First pass binary-search-on-answer, hash-table bug-fix, and bucket-based top-k as separate focused gates with no blanks. |
| 14 | LRU Cache fix + Graph Representation (RESTRUCTURED) | — | — |
| 15 | Graph Algorithms (ADAPTED) | — | — |
| 16 | Dynamic Programming (ADAPTED) | — | Memoize wrapper — failed in march-13, march-15 |
| 17 | Strings (ADAPTED) | — | — |
| 18 | Bit Manipulation + Complexity Justification (ADAPTED) | — | — |
| 19 | OOP (ADAPTED) | — | Fix march-15 Q7 withdraw logic |
| 20 | System Design + Verbal Review (ADAPTED) | — | — |
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
