# APRIL 6 ASSESSMENT | ANSWER SHEET
**Date:** April 6, 2026
**For:** Examiner / self-check use only. Do not show to candidate before submission.

---

## SECTION A: FOUNDATIONS (25 marks)

---

### Q1. Closures and Scope (10 marks)

**Part A — Output prediction (4 marks)**

```
12
1
false
```

Line-by-line reasoning:
- `makeCounter(10)` creates closure `a` with its own private `count = 10`.
- `makeCounter(0)` creates a separate closure `b` with its own private `count = 0`.
- Each returned object holds a reference to its own enclosed `count` — they do not share state.
- `a.increment()` twice: `count` in `a` goes 10 → 11 → 12. `a.value()` → `12`.
- `b.increment()` once: `count` in `b` goes 0 → 1. `b.value()` → `1`.
- `a === b` → `false` — they are two different objects returned by two separate calls.

**Part B — Two fixes (4 marks)**

Fix 1 — `let`:
```javascript
const fns = [];
for (let i = 0; i < 5; i++) {
  fns.push(function() { return i; });
}
```
`let` creates a new binding per iteration. Each closure captures its own `i`.

Fix 2 — IIFE closure:
```javascript
const fns = [];
for (var i = 0; i < 5; i++) {
  fns.push((function(captured) {
    return function() { return captured; };
  })(i));
}
```
The IIFE is called immediately with the current value of `i`, creating a new scope with `captured` fixed to that value. The inner function closes over `captured`, not `i`.

**Part C — Explanations (2 marks)**

1. `var` is function-scoped, not block-scoped. All five closures share the same single `i` variable. By the time any `fns[n]()` is called, the loop has finished and `i === 5`. Every closure reads the same final value.

2. `let` is block-scoped. Each iteration of the loop creates a fresh binding for `i`. The closure captures that iteration's own copy of `i`, so each function holds a different value.

---

### Q2. Big O Complexity (5 marks)

**Snippet A — `hasPair`**
- Time: **O(n)** — one pass through the array; each `Set.has()` and `Set.add()` is O(1) on average, so the loop is O(n) total.
- Space: **O(n)** — the `Set` can grow to hold every element in the worst case (no pair found).

**Snippet B — `allPairs`**
- Time: **O(n²)** — the outer loop runs n times; the inner loop runs up to n-1 times per outer iteration, producing roughly n²/2 iterations total.
- Space: **O(n²)** — the `result` array holds one entry per pair, and there are n*(n-1)/2 pairs.

**Snippet C — `countBits`**
- Time: **O(log n)** — the loop runs once per bit in the binary representation of `n`; an integer `n` has ⌊log₂(n)⌋ + 1 bits.
- Space: **O(1)** — only two integer variables regardless of input size.

---

### Q3. Group Anagrams (10 marks)

```javascript
function groupAnagrams(words) {
  const map = new Map();

  for (const word of words) {
    const key = word.split("").sort().join("");

    if (!map.has(key)) {
      map.set(key, []);
    }
    map.get(key).push(word);
  }

  return Array.from(map.values());
}
```

**Edge cases handled:**
- `[""]` → key is `""`, one group `[[""]]`
- `["a"]` → key is `"a"`, one group `[["a"]]`

**Complexity:**
- Time: **O(n · k log k)** where n is the number of words and k is the maximum word length. Each word is sorted (k log k) and inserted into the map (O(1) amortised), giving O(n · k log k) total.
- Space: **O(n · k)** — the map stores every character of every word across all groups.

**Key choice explanation:**
The key is the sorted characters of the word (e.g. `"eat"` → `"aet"`). Any two words that are anagrams produce the exact same sorted string, so they map to the same group. Words that are not anagrams sort to different strings and land in different groups.

---

## SECTION B: CORE DATA STRUCTURES & ALGORITHMS (45 marks)

---

### Q4. Trees and Queues (15 marks)

**Part A — Level-Order Traversal (8 marks)**

```javascript
function levelOrder(root) {
  if (!root) return [];

  const result = [];
  const queue = [root];

  while (queue.length > 0) {
    const levelSize = queue.length;
    const level = [];

    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift();
      level.push(node.val);
      if (node.left)  queue.push(node.left);
      if (node.right) queue.push(node.right);
    }

    result.push(level);
  }

  return result;
}
```

For the given tree: `[[5], [3, 8], [1, 4, 9]]`

**Complexity:**
- Time: **O(n)** — every node is enqueued and dequeued exactly once.
- Space: **O(n)** — the queue holds at most one full level at a time; the widest level of a complete binary tree holds n/2 nodes.

**Queue vs stack:**
A queue processes nodes in FIFO order — when a node is dequeued, its children are added to the back. All nodes at depth d are processed before any node at depth d+1 because they were enqueued first. A stack would process the most recently added child first, diving deep before exploring siblings, producing DFS (depth-first) order instead.

**Part B — Validate BST (7 marks)**

```javascript
function isValidBST(root, min = -Infinity, max = Infinity) {
  if (!root) return true;
  if (root.val <= min || root.val >= max) return false;

  return isValidBST(root.left,  min,       root.val) &&
         isValidBST(root.right, root.val,  max);
}
```

**Counterexample — passes naive check, fails correct validation:**
```
    5
   / \
  1   7
     / \
    4   9
```
Node 4 is in the right subtree of 5 but is less than 5 — invalid BST. A naive check only compares 7 with its children (4 < 7 ✓, 9 > 7 ✓) and misses the violation. The correct approach passes `min` and `max` bounds down every recursive call — the right child of 5 must be greater than 5, so 4 is immediately caught when its max bound is 5.

---

### Q5. Graph — BFS and Topological Sort (15 marks)

**Part A — BFS Traversal (4 marks)**

BFS order from `"A"`: `A, B, C, D, E, F`

Queue state at each step:
1. Start: queue = `[A]`
2. Dequeue A, enqueue B, C → queue = `[B, C]`
3. Dequeue B, enqueue D → queue = `[C, D]`
4. Dequeue C, enqueue D (already visited, skip), enqueue E → queue = `[D, E]`
5. Dequeue D, enqueue F → queue = `[E, F]`
6. Dequeue E, enqueue F (already visited, skip) → queue = `[F]`
7. Dequeue F, no unvisited neighbours → queue = `[]`

Visit order: `A B C D E F`

**Shortest-path guarantee:** BFS expands nodes in waves of increasing distance from the source — all nodes at distance d are fully processed before any node at distance d+1 is visited, so the first time a node is reached it is via the shortest possible path.

**Part B — Topological Sort (11 marks)**

**Algorithm description (before code):**
Build an in-degree map counting how many prerequisites each task has. Load all tasks with in-degree 0 into a queue — these can start immediately. Repeatedly dequeue a task, add it to the result, and decrement the in-degree of all its dependents; if a dependent's in-degree reaches 0, enqueue it. If the result contains all tasks the order is valid; if not, a cycle exists.

```javascript
function buildOrder(numTasks, deps) {
  const inDegree = new Array(numTasks).fill(0);
  const adj = Array.from({ length: numTasks }, () => []);

  for (const [task, prereq] of deps) {
    adj[prereq].push(task);
    inDegree[task]++;
  }

  const queue = [];
  for (let i = 0; i < numTasks; i++) {
    if (inDegree[i] === 0) queue.push(i);
  }

  const order = [];
  while (queue.length > 0) {
    const task = queue.shift();
    order.push(task);

    for (const next of adj[task]) {
      inDegree[next]--;
      if (inDegree[next] === 0) queue.push(next);
    }
  }

  return order.length === numTasks ? order : [];
}
```

**Trace for `numTasks=6, deps=[[2,0],[3,1],[4,2],[4,3],[5,4]]`:**

After building adjacency list and in-degrees:
- adj: `{ 0:[2], 1:[3], 2:[4], 3:[4], 4:[5], 5:[] }`
- inDegree: `[0, 0, 1, 1, 2, 1]`

Initial queue (in-degree 0): `[0, 1]`

| Dequeue | Enqueue | inDegree update | order so far |
|---|---|---|---|
| 0 | 2 (0→1-1=0, enqueue) | inDegree[2]=0 | [0] |
| 1 | 3 (1→1-1=0, enqueue) | inDegree[3]=0 | [0,1] |
| 2 | — (inDegree[4]: 2→1) | inDegree[4]=1 | [0,1,2] |
| 3 | 4 (inDegree[4]: 1→0, enqueue) | inDegree[4]=0 | [0,1,2,3] |
| 4 | 5 (inDegree[5]: 1→0, enqueue) | inDegree[5]=0 | [0,1,2,3,4] |
| 5 | — | — | [0,1,2,3,4,5] |

Result: `[0,1,2,3,4,5]` — length 6 = numTasks → valid, no cycle.

---

### Q6. Dynamic Programming and Sliding Window (15 marks)

**Part A — House Robber (8 marks)**

**Recurrence:** `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`

```javascript
function rob(nums) {
  if (nums.length === 0) return 0;
  if (nums.length === 1) return nums[0];

  let prev2 = nums[0];
  let prev1 = Math.max(nums[0], nums[1]);

  for (let i = 2; i < nums.length; i++) {
    const current = Math.max(prev1, prev2 + nums[i]);
    prev2 = prev1;
    prev1 = current;
  }

  return prev1;
}
```

**Complexity:**
- Time: **O(n)** — one pass through the array.
- Space: **O(1)** — only two rolling variables, not a full dp array.

**Why greedy fails:**
Greedy would pick the larger of each adjacent pair, but that can lock you out of a better non-adjacent combination. Counterexample: `[2, 1, 1, 2]` — greedy picks index 0 (2) then skips index 1 (1) and takes index 2 (1) → total 3. The correct answer picks index 0 and index 3: 2 + 2 = 4. The globally optimal choice requires looking ahead, which greedy cannot do.

**Part B — Sliding Window Explanation (7 marks)**

**Step-by-step trace for `nums = [3, 1, 4, 1, 5, 9, 2, 6], k = 3`:**

| Window indices | Values | Sum | Max so far |
|---|---|---:|---:|
| [0..2] | 3, 1, 4 | 8 | 8 |
| [1..3] | 1, 4, 1 | 6 | 8 |
| [2..4] | 4, 1, 5 | 10 | 10 |
| [3..5] | 1, 5, 9 | 15 | 15 |
| [4..6] | 5, 9, 2 | 16 | 16 |
| [5..7] | 9, 2, 6 | 17 | 17 |

Maximum sum: **17** (window at indices 5–7)

**Window invariant:** The window always contains exactly k consecutive elements. At each step the sum is maintained by subtracting the element that leaves the left edge and adding the element entering the right edge — constant work per slide.

**When the window slides:** After the initial window of size k is formed, the window slides by one position each iteration: left pointer advances by 1, right pointer advances by 1.

**Complexity:**
- Time: **O(n)** — the right pointer visits each element once and the left pointer follows; each element is added and removed from the running sum at most once.
- Space: **O(1)** — only the running sum and the maximum are tracked; the window is represented by two indices.

**Adapting to variable window (longest substring without repeating characters):**
The one key difference is the shrink condition: a fixed window always slides by exactly 1 when it reaches size k, but a variable window shrinks from the left whenever a character is repeated — the left pointer advances until the duplicate is removed, making the window size dynamic rather than fixed.

---

## SECTION C: OOP, REFACTORING AND DESIGN PATTERNS (20 marks)

---

### Q7. OOP and Refactoring (10 marks)

**Part A — Two smells (4 marks)**

**Smell 1:**
- Category: **OO Abuser**
- Smell: **Switch Statements** (type-code switching on `report.type`)
- Technique: **Replace Type Code with Subclasses** — create a subclass per report type that overrides the type-labelling behaviour, eliminating the chain of `if` checks

**Smell 2:**
- Category: **Bloater**
- Smell: **Long Method** — `generate()` does validation, formatting, type-labelling, and three different output operations in one method
- Technique: **Extract Method** — pull each cohesive block into its own named method (`validate`, `format`, `output`)

Accept either of these as the second smell (both are valid):
- Category: **Change Preventer** / Smell: **Divergent Change** — the class changes when a new report type is added AND when the output channels change
- Technique: **Extract Class** — separate the output strategy from the report formatting

**Part B — Refactored code (6 marks)**

```javascript
// Base class — no type switching, no output logic
class Report {
  constructor(title, data) {
    this.title = title;
    this.data = data;
  }

  validate() {
    if (!this.title) throw new Error("Missing title");
    if (!this.data || this.data.length === 0) throw new Error("No data");
  }

  typeLabel() {
    throw new Error("typeLabel() must be implemented by subclass");
  }

  format() {
    let output = `=== ${this.title} ===\n`;
    for (const row of this.data) {
      output += `${row.label}: ${row.value}\n`;
    }
    output += `Type: ${this.typeLabel()}\n`;
    return output;
  }
}

// Concrete report types — each owns its label, nothing else changes
class SalesReport   extends Report { typeLabel() { return "Sales Report"; } }
class FinanceReport extends Report { typeLabel() { return "Finance Report"; } }
class HRReport      extends Report { typeLabel() { return "HR Report"; } }

// Generator — only orchestrates, does not know report types
class ReportGenerator {
  generate(report) {
    report.validate();
    const output = report.format();

    console.log(output);
    fs.writeFileSync(`${report.title}.txt`, output);
    sendToSlack(output);

    return output;
  }
}
```

Adding a new report type now means adding one new subclass. `ReportGenerator` does not change. This satisfies the Open/Closed Principle.

---

### Q8. Observer — Order System (10 marks)

```javascript
class OrderSystem {
  constructor() {
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter(o => o !== observer);
  }

  placeOrder(orderId) {
    for (const observer of this.observers) {
      observer.notify(orderId);
    }
  }
}

// Concrete observers
class InventoryService {
  notify(orderId) {
    console.log(`[Inventory] Reducing stock for order #${orderId}`);
  }
}

class EmailService {
  notify(orderId) {
    console.log(`[Email] Confirmation sent for order #${orderId}`);
  }
}

class AnalyticsService {
  notify(orderId) {
    console.log(`[Analytics] Order #${orderId} recorded`);
  }
}

// Usage example
const store = new OrderSystem();
const inventory = new InventoryService();
const email     = new EmailService();
const analytics = new AnalyticsService();

store.subscribe(inventory);
store.subscribe(email);
store.subscribe(analytics);

store.placeOrder(101);
// [Inventory] Reducing stock for order #101
// [Email] Confirmation sent for order #101
// [Analytics] Order #101 recorded

store.unsubscribe(email);

store.placeOrder(102);
// [Inventory] Reducing stock for order #102
// [Analytics] Order #102 recorded
```

**Participant mapping:**
- **Subject** (interface) → the role played by `OrderSystem` (manages subscribers, triggers notifications)
- **ConcreteSubject** → `OrderSystem` (the actual implementation)
- **Observer** (interface) → the `notify(orderId)` contract shared by all three services
- **ConcreteObserver** → `InventoryService`, `EmailService`, `AnalyticsService`

**Why OrderSystem does not need to reference InventoryService directly:**
`OrderSystem` only calls `observer.notify(orderId)` — it depends on the method contract, not on the concrete class, so any object with a `notify` method can be subscribed without changing `OrderSystem`.

---

## SECTION D: SYSTEM DESIGN (10 marks)

---

### Q9. System Design Concepts (10 marks)

**Part A — CAP Theorem (4 marks)**

The CAP theorem states that a distributed system can guarantee at most two of three properties simultaneously: Consistency (all nodes return the same data), Availability (every request gets a response), and Partition Tolerance (the system works despite network failures).

| Pair | What it sacrifices | Real database example | One-sentence justification |
|---|---|---|---|
| CP | Availability | HBase | During a network partition HBase refuses reads rather than return stale data — acceptable for financial systems where incorrect data is worse than no data |
| AP | Consistency | Cassandra | During a partition Cassandra returns the best available data even if slightly stale — acceptable for social feeds where a briefly outdated timeline is harmless |
| CA | Partition Tolerance | PostgreSQL (single-node) | A single-node relational DB is consistent and available but cannot survive network partitions because it has nowhere to partition to |

**Part B — Caching (3 marks)**

1. **Cache-aside** (lazy loading) — the application checks the cache first; on a miss it fetches from the database, writes to the cache, and returns the result.

2. On a cache miss: the application queries the database directly, writes the result into the cache with a TTL (time-to-live), then returns it to the caller.

3. **Dangerous scenario:** If a product's price is updated in the database but the cached version has not yet expired, customers see the wrong (stale) price. For a flash sale or a correction after a pricing error, this window of inconsistency causes real financial or legal harm.

**Part C — Rate Limiter (3 marks)**

```javascript
class RateLimiter {
  constructor(maxRequests, windowMs) {
    this.maxRequests = maxRequests;
    this.windowMs    = windowMs;
    this.timestamps  = new Map(); // userId -> number[]
  }

  allow(userId) {
    const now         = Date.now();
    const windowStart = now - this.windowMs;

    if (!this.timestamps.has(userId)) {
      this.timestamps.set(userId, []);
    }

    // Prune timestamps outside the current window
    const recent = this.timestamps.get(userId).filter(t => t > windowStart);
    this.timestamps.set(userId, recent);

    if (recent.length < this.maxRequests) {
      recent.push(now);
      return true;
    }

    return false;
  }
}
```

**Complexity:**
- Time: **O(k)** per call where k is the number of stored timestamps for that user — bounded by `maxRequests` in practice, so effectively O(1).
- Space: **O(U × maxRequests)** where U is the number of distinct users tracked — each user's array is capped at `maxRequests` entries after pruning.

---

## MARKS BREAKDOWN

| Section | Q | Topic | Max | Notes |
|---|---|---|---:|---|
| A | 1a | Closure output prediction | 4 | 1 per line explained correctly |
| A | 1b | Two loop fixes | 4 | 2 per fix |
| A | 1c | Two explanations | 2 | 1 each |
| A | 2 | Big O (3 snippets) | 5 | ~1.5 per snippet; justification mandatory |
| A | 3 | Group anagrams | 10 | 5 code, 3 complexity, 2 key explanation |
| B | 4a | Level-order traversal | 8 | 5 code, 2 complexity, 1 queue vs stack |
| B | 4b | isValidBST | 7 | 4 code, 3 counterexample + explanation |
| B | 5a | BFS trace | 4 | 2 order, 1 queue trace, 1 explanation |
| B | 5b | Topological sort | 11 | 3 description, 6 code, 2 trace |
| B | 6a | House robber | 8 | 1 recurrence, 5 code, 2 complexity + greedy |
| B | 6b | Sliding window explanation | 7 | 3 trace, 2 invariant, 1 complexity, 1 variable |
| C | 7a | Two smells | 4 | 2 per smell (category + name + technique) |
| C | 7b | Refactored code | 6 | 3 subclasses, 2 generator, 1 OCP explanation |
| C | 8 | Observer implementation | 10 | 5 code, 3 usage trace, 2 mapping + explanation |
| D | 9a | CAP theorem | 4 | 1 definition, 3 table rows |
| D | 9b | Caching | 3 | 1 pattern, 1 miss, 1 dangerous scenario |
| D | 9c | Rate limiter | 3 | 2 code, 1 complexity |
| **Total** | | | **100** | |
