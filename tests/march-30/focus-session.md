# FOCUS SESSION | MARCH 30 FOLLOW-UP
**Date:** March 30, 2026  
**Reason:** The March 30 cumulative paper showed small improvement, but fresh transfer still broke on binary-search-on-answer, topological sort, sliding window, and exact behavior contracts.

---

## Goal

Turn pattern recognition into exact, testable implementation on the specific misses from the March 30 paper.

## Session Rules

1. No blanks.
2. Before writing code, say the approach in 2-3 sentences.
3. Before finalizing code, check:
   one normal case, one smallest edge case, and one tricky boundary case.
4. Read variable names, return values, and required behavior line by line before submitting.

## Block 1: Binary Search On Answer

### Drill

Re-solve:

```javascript
function shipWithinDays(weights, days) {
  // TODO
}
```

### Must say out loud first

- Search space:
  `max(weights)` through `sum(weights)`
- Yes/no check:
  "Can I ship all packages within `days` if the capacity is `mid`?"
- Binary-search rule:
  if `mid` works, keep it and search left with `high = mid`

### Self-check

- Normal case:
  `[3,2,2,4,1,4], days = 3`
- Edge case:
  `days = weights.length`
- Boundary case:
  `days = 1`

## Block 2: Topological Sort

### Drill

Re-solve:

```javascript
function findBuildOrder(numTasks, deps) {
  // TODO
}
```

### Must say out loud first

- Data structures:
  adjacency list, in-degree array, queue
- Why it works:
  only tasks with in-degree `0` are ready
- Cycle rule:
  if output length is smaller than `numTasks`, return `[]`

### Self-check

- Normal case:
  `[[1,0],[2,0],[3,1],[3,2],[4,3]]`
- Edge case:
  `deps = []`
- Boundary case:
  cycle like `[[0,1],[1,0]]`

## Block 3: Fixed-Size Sliding Window

### Drill

Re-solve:

```javascript
function checkInclusion(s1, s2) {
  // TODO
}
```

### Must say out loud first

- Window length must stay exactly `s1.length`
- One character enters, one character leaves
- Compare frequency state, not character-by-character positions

### Self-check

- Normal case:
  `"ab", "eidbaooo"`
- Negative case:
  `"ab", "eidboaoo"`
- Boundary case:
  `s1.length > s2.length`

## Block 4: Contract Precision

### Drill

Rewrite the March 30 `Wallet` / `CashbackWallet` answer and verify:

- `deposit(amount)` rejects non-positive input
- `spend(amount)` throws an error when `amount > balance`
- `getBalance()` returns the raw current balance
- `applyCashback(percent)` increases the balance by that percentage

### Self-check

- Deposit positive amount
- Spend exact balance
- Spend more than balance
- Apply cashback after a spend

## Exit Gate

This follow-up counts as successful only if:

1. every question has a complete attempt,
2. the implementation runs in principle,
3. the explanation matches the actual code,
4. and the complexity / contract statements are checked before submission.
