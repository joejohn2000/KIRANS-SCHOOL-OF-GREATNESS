# EVALUATION SCORE | MARCH 27 RETEST DAY 11-12 RECOVERY GATE
**Evaluation Date:** March 28, 2026  
**Test Date:** March 27, 2026  
**Student Answer Source:** `tests/march-27-2nd/candidate-answers.md`  
**Focus:** Stack precision, queue using two stacks, monotonic stack tracing, BST complexity, and bounds-based BST validation  
**Overall Result:** 45/70 - Partial recovery, but gate not yet cleared  

---

## Scoring Summary

| Section | Max Marks | Marks Awarded |
|---|---:|---:|
| Section A: Stack and Queue Precision | 30 | 17 |
| Section B: Monotonic Stack Trace | 12 | 8 |
| Section C: BST Gate | 28 | 20 |
| **Total** | **70** | **45** |

---

## Question-by-Question Breakdown

| Question | Max Marks | Marks Awarded | Comments |
|---|---:|---:|---|
| Q1 | 10 | 6 | `push(item)` and the complexity answers were corrected, which is good progress. `peek()` still used the wrong property (`item` instead of `items`) and `size()` returned `length - 1`, so the implementation was still not correct. |
| Q2 | 20 | 11 | The overall queue structure and the amortized idea improved, and `empty()` was correct. But `push()` still used the wrong property name (`instack`), `peek()` used `pop` instead of `pop()`, and `peek()` never returned the front value. |
| Q3 | 12 | 8 | The core algorithm improved a lot and the explanation of why indices matter was much better. The final output still had one wrong value (`0` instead of `1` at index 4), and the trace used temperatures rather than a correct stack-of-indices trace. |
| Q4 | 10 | 9 | Balanced and unbalanced BST complexities were corrected, and the degeneration idea was right. The concrete example should have been given as a proper insertion sequence rather than an invalid BST drawing. |
| Q5 | 18 | 11 | There was real improvement here: the student used min/max bounds and propagated bounds to child calls. But the failing tree example was not actually a failing example, the code had a `rol` typo, and the complexity discussion should have used `O(h)` for space with worst-case clarification. |

---

## Strengths Demonstrated

- Recovery work clearly helped; this retest was stronger than the first March 27 checkpoint.
- Balanced vs unbalanced BST complexity is now much closer to stable.
- The monotonic-stack idea improved meaningfully.
- The student now has the right broad idea for bounds-based BST validation.

## Areas For Growth

- Queue implementation still breaks on exact property names and exact method calls.
- The student still needs to return the correct value from `peek()` rather than only performing transfer logic.
- Daily Temperatures trace work is still not exact enough under pressure.
- Concrete counterexamples are still weak: the BST failing-tree example was not actually failing.
- Final correctness still drops because of small implementation slips (`items` vs `item`, `pop` vs `pop()`, `rol` typo).

## Evidence-Based Notes

- This was a real improvement over the earlier March 27 checkpoint, but it was not a full recovery.
- The student's understanding is moving in the right direction faster than their code accuracy.
- Day 11 is still the main blocker because `MyQueue` is not yet reliable enough to count as passed.
- Day 12 is closer, but `isValidBST` still needs one more exact, correct pass.

## Recommendation

**Recommendation:** Partial recovery only.  
Do **not** start the full Day 13 heaps workload yet.

Allow only a short final recovery block focused on:
- `MyQueue` end-to-end correctness
- exact stack trace discipline for Daily Temperatures
- one fully correct `isValidBST` solution with a real failing counterexample

If those 3 are clean on the next try, the student can continue with Day 13 carry-over.

## Next Action

1. Re-write `MyQueue` with exact property names and `pop()` / `peek()` behavior.
2. Re-do the Daily Temperatures trace using indices, not temperatures.
3. Write one real failing BST example and one typo-free bounds-based `isValidBST`.
