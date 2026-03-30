# EVALUATION SCORE | MARCH 28 ASSESSMENT THROUGH DAY 13
**Evaluation Date:** March 30, 2026  
**Test Date:** March 28, 2026  
**Student Answer Source:** `tests/march-28-2nd/candidate-answers.md`  
**Focus:** Fresh transfer questions covering Day 11, Day 12, and Day 13 content  
**Overall Result:** 30/100 - Not ready to widen scope  

---

## Scoring Summary

| Section | Max Marks | Marks Awarded |
|---|---:|---:|
| Section A: Stacks and Queues - Fresh Applications | 25 | 9 |
| Section B: Trees and BSTs - Fresh Questions | 25 | 16 |
| Section C: Day 13 Carry-Over + Heaps Thinking | 50 | 5 |
| **Total** | **100** | **30** |

---

## Question-by-Question Breakdown

| Question | Max Marks | Marks Awarded | Comments |
|---|---:|---:|---|
| Q1 | 15 | 7 | The two-stack min idea was recognized and `push`, `top`, and `getMin` were directionally correct. But `pop()` had broken syntax, wrong property names, and invalid empty-check logic, so the implementation would not run. |
| Q2 | 10 | 2 | The queue idea was recognized at the explanation level, but the class implementation was fundamentally broken: wrong property names, wrong return value, and invalid setup. |
| Q3 | 10 | 7 | The level-order traversal was correct. The queue explanation showed the FIFO idea, but it was imprecise and mixed in unclear wording. |
| Q4 | 15 | 9 | The placement explanation for inserting `13` was correct, and the balanced vs unbalanced complexities were correct. The implementation itself was broken: wrong comparisons, wrong recursive calls, and invalid node construction. |
| Q5 | 20 | 2 | This did not solve the binary-search-on-answer problem. The answer used a single pass with the maximum divisor and did not search the answer space. The stated complexity matched the incorrect code, not the required solution. |
| Q6 | 15 | 0 | No answer was provided. |
| Q7 | 15 | 3 | Frequency counting was correct and the final extraction idea returned something plausible for top-k. But it did not follow the required bucket approach, and the explanation incorrectly claimed O(n). The solution sorts repeatedly, so it does not meet the prompt. |

---

## Strengths Demonstrated

- The student can still recognize core data-structure patterns.
- Tree / BST conceptual understanding is stronger than queue / heap / hash-table implementation.
- Placement reasoning inside a BST is improving.

## Areas For Growth

- Fresh transfer to new questions is still weak.
- Implementation still breaks on exact method calls, exact property names, and exact comparisons.
- Day 13 carry-over topics are not ready yet:
  binary-search-on-answer, hash-table debugging, and bucket-based top-k thinking all remain weak.
- The student is still much stronger at recognizing a pattern than finishing a correct implementation.
- Blank answers are still costly and must stop.

## Evidence-Based Notes

- This score is much lower than the narrow March 27 recovery retest, which means isolated remediation is helping, but broad transfer to fresh problems is not stable yet.
- Day 11 and Day 12 are not fully consolidated, and the jump into Day 13-style fresh applications exposed that clearly.
- The student is not yet ready for a wider Day 13 progression.

## Recommendation

**Recommendation:** Do not widen scope.  
Return to a structured carry-over path before attempting another broad Day 13 paper.

Priority order:
1. Perfect exact queue / stack implementation on fresh prompts
2. Solid BST insertion and validation code on fresh prompts
3. Binary-search-on-answer pattern from scratch
4. Hash-table bug fixing
5. Bucket-based top-k thinking

## Next Action

1. Run a focused Day 13 carry-over block instead of another broad mixed assessment.
2. Ban blanks: every question must have an attempt.
3. Re-test binary-search-on-answer and hash-table debugging separately before another cumulative paper.
