# Student Progress Card

This file is a running memory of the student's strengths, weaknesses, and learning pattern based on actual test submissions and scored evaluations found in this repo.

## Evidence Used

- March 13, 2026: Days 1-2 assessment (`tests/march-13`)
- March 14, 2026: JavaScript deep dive (`tests/march-14`)
- March 15, 2026: JavaScript fundamentals deep dive (`tests/march-15`)
- March 22, 2026: Days 1-7 review (`tests/march-22`, plus documented score in `progress-card-march-22.md`)
- March 22/23, 2026: Medium tricky focus answers (`tests/march-22-2nd`)
- March 27, 2026: Day 11-12 checkpoint (`tests/march-27`)
- March 28, 2026: March 27 recovery retest (`tests/march-27-2nd`)
- March 30, 2026: Broad fresh paper through Day 13 (`tests/march-28-2nd`)

Note: `tests/march-23` and `tests/march-24` contain question papers / answer keys, but no clear student submission was found there, so they are not treated as performance evidence.

## Score Trend

| Date | Assessment | Result | Read |
|---|---|---:|---|
| March 13, 2026 | Days 1-2 assessment | 40/100 | Early gaps in core concepts and very weak coding implementation |
| March 14, 2026 | JavaScript assessment | 36/100 | Scope basics visible, but closures and event loop still weak |
| March 15, 2026 | JS fundamentals deep dive | 57/103 (~55%) | Clear improvement, especially in event loop tracing |
| March 22, 2026 | Days 1-7 review | 70/100 | Satisfactory recovery in core fundamentals |
| March 22/23, 2026 | Medium tricky focus | No official score file, but answers were mostly correct | Attention to detail improved, with a few edge-case misses still present |
| March 27, 2026 | Day 11-12 checkpoint | 48/100 | Tree traversal and recursion showed progress, but stack/queue implementation and BST reasoning were not ready |
| March 28, 2026 | March 27 recovery retest | 45/70 | Clear improvement after focused study, but queue correctness and exact BST validation still blocked a full pass |
| March 30, 2026 | Broad fresh paper through Day 13 | 30/100 | Narrow recovery did not yet transfer to fresh questions, especially on Day 13 carry-over content |

## Current Snapshot

The student has a real upward trend. Concept understanding has improved faster than implementation reliability.

Right now, the student is stronger at:
- tracing code,
- recognizing the right concept or pattern,
- and explaining what should happen,

than at:
- writing clean working code from scratch,
- handling edge cases,
- and catching small syntax / logic mistakes before submission.

## Reliable Strengths

- Learns quickly after focused remediation.
- Scope chain and lexical scoping basics are now fairly stable.
- Can often predict output correctly when the pattern is familiar.
- Event loop understanding improved sharply by March 15.
- Big O basics are solid enough for simple loop analysis.
- Recognizes when to use two pointers and hash maps.
- Understands recursion at a concept level, especially the need for a base case.
- Sorting theory is better than sorting implementation.
- Recent tricky-question performance suggests better attention to detail than the early tests.
- Tree traversal order and basic recursive tree implementation are becoming reliable.
- Focused remediation does help quickly when the weak area is narrow and concrete.
- Recognizes broad solution shapes even when final fresh implementations still break.

## Recurring Weaknesses

- Translating concepts into correct code is still the main blocker.
- Closure-heavy implementation remains a weak area:
  module pattern, curry, memoization, private-state utilities, stack-with-closures.
- Edge cases still cause avoidable errors:
  empty arrays, sparse arrays, off-by-one boundaries, missing base cases, floating-point quirks.
- Mutation / reference behavior is inconsistent:
  especially Python references/copies and in-place updates.
- Small implementation slips cost a lot of marks:
  missing `return`, wrong method names, wrong variable in a condition, wrong loop bounds, missing commas/braces, `If` vs `if`.
- Student sometimes knows the expected output but cannot build the function that produces it.
- Self-checking is not yet strong enough; code is often not verified against the sample cases before submission.
- Data-structure implementation is still fragile under pressure:
  wrong property names, wrong state updates, and incorrect method calls can break otherwise familiar patterns.
- BST reasoning is mixed:
  traversals are good, but balanced-vs-unbalanced complexity and bounds-based validation are still unstable.
- Small typos and off-by-one slips still turn near-correct answers into wrong final answers.
- Transfer to fresh prompts is still weak:
  the student improves on tightly targeted recovery, but performance drops when multiple patterns are mixed into a broader paper.

## Strongest Evidence-Based Topic Signals

- Event loop: major improvement.
  March 14 was a complete miss on the async order question; by March 15 the event-loop section was strong (`22/25`).
- Review topics from Days 1-7: meaningful recovery.
  By March 22 the student was comfortable with Big O basics, two-pointer recognition, hash map use cases, recursion basics, and some sorting theory.
- Tricky code reading: improving.
  In the medium tricky focus paper, most answers were correct. The clearest remaining misses were an empty-array edge case (`Math.max(...[])`) and one microtask-order detail.
- Trees: improving, but uneven.
  March 27 showed strong traversal recall and a mostly correct recursive `maxDepth`, but BST complexity and range-based validation still broke under pressure.
- Recovery speed: encouraging, but not complete.
  The March 28 retest showed the student can improve noticeably after a focus session, but exact queue correctness and typo-free BST validation are still the final blockers.
- Broad transfer: not ready yet.
  The March 30 evaluation showed that fresh Day 13-style problems still expose major instability, especially binary-search-on-answer, hash-table debugging, and bucket-based top-k work.

## Stable Memory for Future Teaching

- This student usually improves when one weak topic is isolated and drilled hard.
- They benefit from tracing first, coding second.
- They do better with pattern templates than with blank-page implementation.
- They are more reliable in multiple-choice / code-reading settings than in open coding.
- If they rush, they lose marks on exactness rather than on broad understanding.

## Best Way to Coach This Student

- Start with: "What should this code do on the sample input?"
- Then ask for the invariant or rule:
  what stays true each loop, recursive call, or pointer move.
- Then make them test 3 cases before finalizing:
  normal case, smallest edge case, and one tricky boundary case.
- For closures / recursion / sorting, use repeatable templates until the structure becomes automatic.
- Ask them to explain why the edge case will not break their code before accepting the answer.

## Priority Practice Next

1. Fresh exact queue / stack implementations:
   `MyQueue`, `RecentCounter`, and `MinStack` with correct property names and return behavior.
2. Fresh BST implementation drills:
   `insertIntoBST` and typo-free `isValidBST`.
3. Binary-search-on-answer from scratch:
   helper predicate, monotonic condition, and correct `low/high` updates.
4. Hash-table bug fixing and bucket-based top-k:
   no blanks, no sorting-all-keys fallback.
5. Tree recursion explanations:
   keep reinforcing correct time/space complexity wording (`O(h)` vs worst-case `O(n)`).
6. Edge-case checklist habit before submitting any answer.

## Bottom Line

The student is improving, and the improvement is real. The biggest gap is no longer "not understanding anything"; it is implementation precision.

In short:
- conceptual understanding is trending upward,
- tracing ability is becoming a strength,
- but exact code writing and edge-case discipline still need repeated practice.

March 27 reinforces the same meta-pattern:
- tree reading and recursive structure are improving,
- but stateful data-structure implementation and exact BST reasoning are still not stable enough to count as mastered.

The March 28 retest adds one more useful signal:
- the student responds well to targeted recovery,
- but "almost correct" is still a real failure mode until the last typos and exact return values are cleaned up.

The March 30 broad paper adds a second useful signal:
- narrow recovery is not yet generalizing,
- so the next step should be structured transfer practice, not a wider jump into new material.
