# MARCH 27 FOCUS SESSION | DAY 11-12 RECOVERY
**Date:** March 27, 2026  
**Reason:** March 27 checkpoint score was 48/100. Implementation precision is still the main blocker.  

---

## What Passed

- Tree traversal orders are solid.
- Recursive `maxDepth` structure is mostly correct.
- The student knows that BST validation needs more than local parent-child checks.

## What Failed And Must Be Fixed First

### 1. Stack / Queue Implementation Precision

Problems seen:
- `push(item)` used `1` instead of `item`
- wrong object properties were used (`items`, `s1`, `s2`)
- `pop()` logic called itself incorrectly
- method behavior and method complexity were mixed up

Why this matters:
- This is not a concept gap only; it is an execution gap.
- These are the exact implementation mistakes that break interview solutions even when the student "knows the idea."

### 2. Monotonic Stack Reasoning

Problems seen:
- output was incomplete
- no valid stack trace was given
- the explanation for storing indices missed the key reason: distance calculation

Why this matters:
- The monotonic stack pattern is not just "use a stack"; it depends on what is stored and why.

### 3. BST Complexity And Degeneration

Problems seen:
- balanced BST complexity was incorrect
- badly unbalanced BST complexity was incorrect
- no clear degeneration pattern or example was finished

Why this matters:
- The student currently recognizes tree structure, but the complexity reasoning is still unstable.

### 4. Validate BST With Bounds

Problems seen:
- min/max idea was recognized
- but the code did not pass updated bounds into child calls
- concrete failing tree example was missing

Why this matters:
- This is a classic "I know the pattern name but not the working implementation" problem.

---

## Today’s Recovery Tasks

### Task 1 - Rebuild Stack Correctly

From memory, write:
- `push`
- `pop`
- `peek`
- `isEmpty`
- `size`

Rule:
- every method must use the correct property name
- `push(item)` must actually use `item`

### Task 2 - Rebuild Queue Using Two Stacks

From memory, write:
- `push`
- `pop`
- `peek`
- `empty`

Then explain in 3 sentences:
- when elements move from `inStack` to `outStack`
- why that transfer does not happen every time
- why the amortized cost is O(1)

### Task 3 - Daily Temperatures Trace

Using `[73,74,75,71,69,72,76,73]`:
- write the final answer array
- trace the stack after each of the first 6 indices
- explain in one sentence why the stack stores indices

### Task 4 - BST Complexity Drill

Write from memory:
- balanced BST search / insert / delete
- unbalanced BST search / insert / delete
- one insertion pattern that causes degeneration
- one concrete example sequence

### Task 5 - Fix `isValidBST`

Write:
- one failing tree for the local-child-check solution
- the corrected min/max solution
- time complexity
- space complexity

---

## Verification Gate

Before moving on, the student must pass all 3:

1. **Queue gate:** write a working `MyQueue` using two stacks without wrong property names.
2. **BST gate:** explain balanced vs unbalanced BST complexity correctly and give a degeneration example.
3. **Validation gate:** write a correct bounds-based `isValidBST` and explain the failing counterexample.

If any of these fail, carry them into the next session before starting heaps.
