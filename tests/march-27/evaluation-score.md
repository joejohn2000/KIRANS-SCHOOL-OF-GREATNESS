# EVALUATION SCORE | MARCH 27 DAY 11-12 CHECKPOINT
**Date:** March 27, 2026  
**Student Answer Source:** `tests/march-27/candidate-answer.md` (canonically transcribed into `tests/march-27/candidate-answers.md`)  
**Focus:** Day 11 and Day 12 - Stacks, Queues, Trees, and BSTs  
**Overall Result:** 48/100 - Not ready to advance  

---

## Scoring Summary

| Section | Max Marks | Marks Awarded |
|---|---:|---:|
| Section A: Stacks and Queues | 45 | 21 |
| Section B: Trees and BSTs | 55 | 27 |
| **Total** | **100** | **48** |

---

## Question-by-Question Breakdown

| Question | Max Marks | Marks Awarded | Comments |
|---|---:|---:|---|
| Q1 | 15 | 10 | Most stack methods were present, but `push(item)` hardcoded `1` instead of using `item`, `pop()` complexity was labeled incorrectly, and the `.peek()` explanation was too vague. |
| Q2 | 18 | 7 | There is partial understanding of the transfer idea from `inStack` to `outStack`, but `push`, `pop`, and `empty` use the wrong properties or invalid calls, so the queue would not work. |
| Q3 | 12 | 4 | Output was incomplete, there was no valid stack trace for indices 0-5, and the explanation of why indices are needed did not mention distance calculation clearly enough. |
| Q4 | 12 | 10 | All four traversals were correct. The BST explanation was directionally right but not precise. |
| Q5 | 10 | 1 | Balanced and unbalanced BST complexities were incorrect, and the degeneration pattern / example were left incomplete. |
| Q6 | 13 | 11 | Recursive solution was correct and the base case was right. Time complexity was correct. Space complexity should have been expressed as `O(h)` rather than only `O(n)`. |
| Q7 | 20 | 5 | The idea of using min/max bounds was recognized, but no concrete failing tree was given, the code used wrong variable names and did not propagate updated bounds to child calls, and space complexity was missing. |

---

## Strengths Demonstrated

- Tree traversal orders are now reliable.
- Recursive tree thinking is improving; `maxDepth` was mostly correct.
- The student recognized that BST validation needs min/max bounds, even though the final implementation was still broken.

## Areas For Growth

- Data-structure implementation precision is still weak under pressure.
- Queue implementation using two stacks is not yet stable.
- Stack method behavior vs method complexity still gets mixed up.
- BST complexity reasoning is unstable, especially balanced vs unbalanced cases.
- The student needs to give concrete failing examples, not just a general description.
- Bound propagation in recursive BST validation needs focused practice.

## Evidence-Based Notes

- This result reinforces the existing pattern: concept recognition is ahead of implementation accuracy.
- Day 12 is mixed: traversal and recursion are showing real progress, but BST reasoning and validation are not stable enough yet.
- Day 11 remains the larger blocker because the student still loses marks on exact state/property handling in stack and queue code.

## Recommendation

**Recommendation:** Repeat Day 11 focus and carry Day 12 BST reasoning into the next session.  
Do **not** move into the full Day 13 heaps workload until:
- `MyQueue` is working end-to-end
- BST balanced vs unbalanced complexity is stated correctly
- `isValidBST` works with propagated min/max bounds

## Next Action

1. Run a short remediation block on stack/queue implementation.
2. Re-do BST complexity and degeneration examples from memory.
3. Fix `isValidBST` with a concrete counterexample and correct bound propagation.
4. Only after that, continue into the next plan segment with carry-over.
