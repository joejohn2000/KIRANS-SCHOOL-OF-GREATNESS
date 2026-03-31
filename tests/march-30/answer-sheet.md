# MARCH 30 ASSESSMENT | ANSWER SHEET
**Date:** March 30, 2026  
**Scope:** Model answers for the cumulative Day 11 through Day 19 paper  

---

## Q1. Browser History Using Stacks (Day 11)

```javascript
class BrowserHistory {
  constructor(homepage) {
    this.backStack = [homepage];
    this.forwardStack = [];
  }

  visit(url) {
    this.backStack.push(url);
    this.forwardStack = [];
  }

  back(steps) {
    while (steps > 0 && this.backStack.length > 1) {
      this.forwardStack.push(this.backStack.pop());
      steps--;
    }

    return this.backStack[this.backStack.length - 1];
  }

  forward(steps) {
    while (steps > 0 && this.forwardStack.length > 0) {
      this.backStack.push(this.forwardStack.pop());
      steps--;
    }

    return this.backStack[this.backStack.length - 1];
  }
}
```

Why stacks fit:
- Back history needs last-in-first-out behavior.
- Forward history also needs last-in-first-out behavior after a back operation.

Complexity:
- `visit`: `O(1)`
- `back`: `O(steps)` in the worst case
- `forward`: `O(steps)` in the worst case

---

## Q2. Lowest Common Ancestor In A BST (Day 12)

```javascript
function lowestCommonAncestor(root, p, q) {
  let current = root;

  while (current) {
    if (p.val < current.val && q.val < current.val) {
      current = current.left;
    } else if (p.val > current.val && q.val > current.val) {
      current = current.right;
    } else {
      return current;
    }
  }

  return null;
}
```

Why BST property helps:
- If both target values are smaller than the current node, the LCA must be in the left subtree.
- If both are larger, the LCA must be in the right subtree.
- The first node where they split, or where one equals the current node, is the LCA.

Complexity:
- Balanced BST: `O(log n)`
- Badly unbalanced BST: `O(n)`

---

## Q3. Binary Search On Answer + Top-K Reasoning (Day 13)

### Part A

```javascript
function shipWithinDays(weights, days) {
  let low = Math.max(...weights);
  let high = weights.reduce((sum, weight) => sum + weight, 0);

  function canShip(capacity) {
    let usedDays = 1;
    let currentLoad = 0;

    for (const weight of weights) {
      if (currentLoad + weight > capacity) {
        usedDays++;
        currentLoad = 0;
      }

      currentLoad += weight;
    }

    return usedDays <= days;
  }

  while (low < high) {
    const mid = Math.floor((low + high) / 2);

    if (canShip(mid)) {
      high = mid;
    } else {
      low = mid + 1;
    }
  }

  return low;
}
```

### Part B

Why this is binary search on answer:
- The answer is not an index; it is a capacity in the range from `max(weights)` to `sum(weights)`.
- `canShip(capacity)` is the yes/no predicate.
- If a capacity works, any larger capacity also works, so we move left with `high = mid` to search for a smaller valid answer.

### Part C

Bucket `topKFrequent` idea:
- Count frequencies with a map.
- Create buckets where index `i` stores all values that appear `i` times.
- Walk the buckets from high frequency to low frequency and collect values until `k` answers are found.
- This avoids sorting all keys, so the overall work can stay linear in the input size.

---

## Q4. Graph Representation + LRU Reasoning (Day 14)

### Part A

Adjacency list:

```javascript
{
  0: [1, 2],
  1: [3],
  2: [4],
  3: [5],
  4: [5],
  5: []
}
```

BFS order from `0`:

```text
0, 1, 2, 3, 4, 5
```

Why queue for BFS:
- BFS visits nodes level by level.
- A queue preserves first-in-first-out order, so earlier discovered nodes are processed before later ones.

### Part B

Why `map.set(key, value)` alone is wrong for an existing key:
- Updating the value does not refresh that key's insertion order in the way the LRU policy needs.
- The correct LRU logic is to remove the old entry and insert it again so it becomes the most recently used entry.

Correct pattern:

```javascript
map.delete(key);
map.set(key, value);
```

---

## Q5. Build Order With Topological Sort (Day 15)

Sample approach note:
- I will build an adjacency list and an in-degree array.
- Then I will use Kahn's algorithm with a queue to repeatedly process tasks whose in-degree is zero.
- This works because a task can only be taken after all prerequisites are removed, and the time complexity is `O(V + E)`.

```javascript
function findBuildOrder(numTasks, deps) {
  const graph = Array.from({ length: numTasks }, () => []);
  const indegree = new Array(numTasks).fill(0);

  for (const [task, prerequisite] of deps) {
    graph[prerequisite].push(task);
    indegree[task]++;
  }

  const queue = [];
  for (let i = 0; i < numTasks; i++) {
    if (indegree[i] === 0) {
      queue.push(i);
    }
  }

  const order = [];
  let index = 0;

  while (index < queue.length) {
    const node = queue[index++];
    order.push(node);

    for (const neighbor of graph[node]) {
      indegree[neighbor]--;
      if (indegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  return order.length === numTasks ? order : [];
}
```

Complexity:
- Time: `O(V + E)` because each node is enqueued once and each edge is processed once.
- Space: `O(V + E)` for the graph, in-degree array, queue, and output.

---

## Q6. Min Cost Climbing Stairs (Day 16)

Recurrence:
- `dp[i] = cost[i] + Math.min(dp[i - 1], dp[i - 2])`

```javascript
function minCostClimbingStairs(cost) {
  const n = cost.length;
  if (n === 2) {
    return Math.min(cost[0], cost[1]);
  }

  const dp = new Array(n);
  dp[0] = cost[0];
  dp[1] = cost[1];

  for (let i = 2; i < n; i++) {
    dp[i] = cost[i] + Math.min(dp[i - 1], dp[i - 2]);
  }

  return Math.min(dp[n - 1], dp[n - 2]);
}
```

Why this is DP:
- The same smaller stair-cost results are reused to build larger answers.
- The best answer for stair `i` depends on optimal answers for `i - 1` and `i - 2`.

Complexity:
- Time: `O(n)` because we fill the DP table once.
- Space: `O(n)` because we store one value per stair.

Acceptable note:
- An `O(1)` extra-space version is also valid if it keeps only the previous two states.

---

## Q7. Permutation In String (Day 17)

```javascript
function checkInclusion(s1, s2) {
  if (s1.length > s2.length) {
    return false;
  }

  const target = new Array(26).fill(0);
  const window = new Array(26).fill(0);
  const base = "a".charCodeAt(0);

  for (const ch of s1) {
    target[ch.charCodeAt(0) - base]++;
  }

  for (let right = 0; right < s2.length; right++) {
    window[s2.charCodeAt(right) - base]++;

    if (right >= s1.length) {
      window[s2.charCodeAt(right - s1.length) - base]--;
    }

    if (arraysEqual(target, window)) {
      return true;
    }
  }

  return false;
}

function arraysEqual(a, b) {
  for (let i = 0; i < 26; i++) {
    if (a[i] !== b[i]) {
      return false;
    }
  }

  return true;
}
```

Why window size stays fixed:
- A permutation of `s1` must use exactly the same number of characters as `s1`.
- So every candidate substring must have length `s1.length`.

Complexity:
- Time: `O(n)` if alphabet size is treated as constant, because each character enters and leaves the window once and the frequency comparison is over 26 letters.
- Space: `O(1)` because the frequency arrays have fixed size 26.

---

## Q8. Missing Number Using XOR Only (Day 18)

```javascript
function missingNumber(nums) {
  let xor = nums.length;

  for (let i = 0; i < nums.length; i++) {
    xor ^= i;
    xor ^= nums[i];
  }

  return xor;
}
```

XOR trace for `[3, 0, 1]`:
- Start: `xor = 3`
- `i = 0`: `xor = 3 ^ 0 ^ 3 = 0`
- `i = 1`: `xor = 0 ^ 1 ^ 0 = 1`
- `i = 2`: `xor = 1 ^ 2 ^ 1 = 2`
- Answer: `2`

Why it works:
- Every number that appears once in the index range and once in the array cancels out because `x ^ x = 0`.
- The only value left after all cancellations is the missing number.

Complexity:
- Time: `O(n)` because the loop visits each array element once and does constant-time XOR work per step.
- Space: `O(1)` because only one accumulator variable is used.

---

## Q9. Wallet And CashbackWallet (Day 19)

```javascript
class Wallet {
  constructor(owner, balance = 0) {
    this.owner = owner;
    this.balance = balance;
  }

  deposit(amount) {
    if (amount <= 0) {
      throw new Error("Deposit must be positive");
    }

    this.balance += amount;
    return this.balance;
  }

  spend(amount) {
    if (amount <= 0) {
      throw new Error("Spend amount must be positive");
    }

    if (amount > this.balance) {
      throw new Error("Insufficient funds");
    }

    this.balance -= amount;
    return this.balance;
  }

  getBalance() {
    return this.balance;
  }
}

class CashbackWallet extends Wallet {
  applyCashback(percent) {
    if (percent < 0) {
      throw new Error("Percent cannot be negative");
    }

    this.balance += (this.balance * percent) / 100;
    return this.balance;
  }
}
```

Why `CashbackWallet` is substitutable:
- It still supports the normal `Wallet` contract: deposit, spend, and get balance all behave as expected.
- It adds extra behavior without breaking the meaning of the inherited methods.

Example LSP violation:
- If a subclass of `Wallet` overrode `spend(amount)` so that it silently allowed overspending into negative balance while callers expected an error on insufficient funds, code written for `Wallet` would break its assumptions.

---

## Quick Marking Notes

- Give strong credit when the candidate chooses the right pattern and the code is mostly correct.
- Deduct heavily for broken invariants, wrong method behavior, or missing complexity reasoning.
- For Q3, do not award full marks if the solution is a one-pass guess instead of binary search on answer.
- For Q5, the answer must actually use in-degree plus queue logic or an equivalent valid topological-sort approach.
- For Q7, a brute-force permutation generator should not receive full credit.
- For Q8, using sorting or a hash set breaks the stated requirement.
