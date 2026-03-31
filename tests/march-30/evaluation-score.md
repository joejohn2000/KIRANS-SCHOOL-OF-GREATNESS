# EVALUATION SCORE | MARCH 30 CUMULATIVE REVIEW THROUGH DAY 19
**Evaluation Date:** March 30, 2026  
**Test Date:** March 30, 2026  
**Student Answer Source:** `tests/march-30/candidate-answers.md`  
**Focus:** Fresh cumulative transfer check across Day 11 through Day 19 topics  
**Overall Result:** 40/100 - Not ready for broader advancement yet  

---

## Scoring Summary

| Section | Max Marks | Marks Awarded |
|---|---:|---:|
| Section A: Days 11-13 Transfer Check | 36 | 16 |
| Section B: Days 14-17 Core Application | 44 | 14 |
| Section C: Days 18-19 Precision And Explanation | 20 | 10 |
| **Total** | **100** | **40** |

---

## Question-by-Question Breakdown

| Question | Max Marks | Marks Awarded | Comments |
|---|---:|---:|---|
| Q1 | 12 | 5 | The answer shows the right browser-history intuition and a workable current-index idea, but it does not satisfy the required stack behavior. `visit(url)` never clears forward history after going back, so the implementation breaks the main invariant of the prompt. |
| Q2 | 10 | 9 | This was strong. The recursive BST logic is correct, the split-point idea is explained clearly, and the balanced vs unbalanced complexity distinction is correct. |
| Q3 | 14 | 2 | This did not solve `shipWithinDays`. The search bounds are wrong, the `canFinish` check is for a different kind of problem, and the binary-search update direction is inverted. The bucket explanation shows a little pattern recognition, but the required Day 13 transfer is still not working from scratch. |
| Q4 | 10 | 5 | The adjacency list and the LRU refresh explanation were directionally correct. But the BFS visit order was missing, and the queue explanation was too imprecise to earn full credit. |
| Q5 | 12 | 0 | No answer was provided. This is costly because topological sort was one of the fresh transfer targets on this paper. |
| Q6 | 12 | 8 | The implementation is close to a valid rolling-DP solution and returns the right answer on the sample shape. Credit was deducted because the recurrence sentence was missing, the declared space complexity was wrong for the actual approach, and the explanation did not clearly state the overlapping-subproblem idea. |
| Q7 | 10 | 1 | The submitted code would not run: `j` is undefined, the control flow is invalid, and the logic does not solve the fixed-size sliding-window problem. Minimal credit only for attempting a time/space discussion. |
| Q8 | 10 | 6 | The XOR implementation is correct and follows the required technique. Marks were lost because the trace is inconsistent with the actual loop bounds, and the "why it works" explanation was not written explicitly enough. |
| Q9 | 10 | 4 | The class structure, inheritance idea, and LSP direction were reasonable. But `deposit` and `spend` use the misspelled variable `amout`, the prompt required throwing an error on overspend, and the contract details were not implemented exactly. |

---

## Strengths Demonstrated

- BST reasoning was the strongest answer on the paper.
- XOR-based missing-number work is now more reliable than before.
- The student still recognizes the intended pattern on many prompts even when the final implementation is incomplete.
- DP structure is improving; the Day 16 answer was much closer to working code than several earlier implementation attempts.

## Areas For Growth

- Fresh implementation precision remains the main blocker.
- Day 13 transfer is still weak:
  `shipWithinDays`, binary-search-on-answer reasoning, and bucket-style top-k explanation are not ready.
- Graph algorithms and string sliding-window work did not transfer on a fresh prompt.
- Blank answers are still too expensive. Q5 was left blank even though the paper explicitly banned blanks.
- Exact contract-following still slips in OOP and data-structure questions:
  required behavior, exact update rules, and error handling need slower checking before submission.

## Evidence-Based Notes

- This is a real improvement over the March 28 fresh transfer paper (`30/100` to `40/100`), so the result is not flat.
- The improvement came mostly from stronger isolated answers like Q2, a closer DP attempt in Q6, and a correct XOR implementation in Q8.
- But the broader conclusion did not change:
  the student is still much more reliable at recognizing the pattern than at delivering typo-free, contract-correct code across a widened mixed paper.
- The same durable weakness remains active:
  narrow recovery can help, but transfer to fresh mixed prompts is still not stable enough to widen scope confidently.

## Recommendation

**Recommendation:** Advance only with heavy carry-over, not a clean advance.  
The next step should be a narrow catch-up block focused on the exact fresh-transfer misses from this paper before any wider Day 14-19 progression is treated as consolidated.

Priority order:
1. Binary-search-on-answer from scratch (`shipWithinDays` style)
2. Topological sort with in-degree plus queue
3. Fixed-size sliding window / permutation checking
4. Contract-accurate class methods and error handling
5. Browser-history state invariants after back/visit/forward

## Next Action

1. Run one focused remediation session covering Q3, Q5, and Q7 first.
2. Keep the "no blanks" rule active and explicit.
3. Require one normal case, one edge case, and one contract check before submission for each coding answer.
