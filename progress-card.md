# Student Learning Memory

`progress-card.md` remains the repo filename for workflow compatibility, but this document is not a report card. It is the durable, evidence-based memory of how this student actually performs under assessment.

Use only actual student submissions and scored evaluations as evidence. Question papers and answer keys are curriculum context, not performance evidence.

## Evidence Ledger

| Date | Evidence | Score / Status | Durable signal |
|---|---|---:|---|
| March 13, 2026 | Days 1-2 assessment (`tests/march-13/evaluation_scoring.md`) | 40/100 | Early gap between code prediction and implementation; closures, Python references, and memoization were weak. |
| March 14, 2026 | JavaScript assessment (`tests/march-14/evaluation_score.md`) | 36/100 | Scope basics were visible, but hoisting, event loop ordering, and closure implementation were still unstable. |
| March 15, 2026 | Day 3 assessment (`tests/march-15/evaluation_score.md`) | 57/103 (~55%) | Real recovery in hoisting and event loop work; closure-heavy implementation still broke. |
| March 22, 2026 | Days 1-7 review (`progress-card-march-22.md`) | 70/100 | Foundations recovered to a satisfactory level; concept recognition was stronger than code accuracy. |
| March 22/23, 2026 | Tricky focus answers only (`tests/march-22-2nd/candidate-answers.md`) | Unscored support evidence | Most tracing answers were correct; attention to detail improved, but this should be treated as light evidence only. |
| March 27, 2026 | Day 11-12 checkpoint (`tests/march-27/evaluation-score.md`) | 48/100 | Tree traversal and recursion improved; queue precision and BST validation were not ready. |
| March 28, 2026 | Day 11-12 recovery gate (`tests/march-27-2nd/evaluation-score.md`) | 45/70 | Focused remediation helped; exact queue behavior and typo-free BST validation still failed the gate. |
| March 30, 2026 | Evaluation of the March 28 fresh paper through Day 13 (`tests/march-28-2nd/evaluation-score.md`) | 30/100 | Narrow recovery did not transfer to fresh mixed prompts; Day 13 carry-over remains active. |
| March 30, 2026 | Cumulative review through Day 19 (`tests/march-30/evaluation-score.md`) | 40/100 | Fresh transfer improved slightly, but broader mixed implementation still breaks; BST reasoning and XOR are improving faster than graph/string/Day 13 execution. |
| April 3, 2026 | Day 20 + Refactoring & Design Patterns deviation (`tests/april-3/evaluation-score.md`) | 37/100 | Smell identification from code is reliable (75% on Q1); system design concepts are solid (65%); but pattern implementation was entirely blank (Q5, Q6 = 0/25) and rate limiter code had 5 structural bugs. Technique name vs smell name confusion is now a documented recurring error. |
| April 3, 2026 (2nd) | Focus gate — patterns + rate limiter (`tests/april-3-2nd/evaluation-score.md`) | 23/50 (46%) | Factory Method structure transferred — went from 0 to a mostly-correct skeleton in one session (largest single improvement recorded). Observer broken by property name mismatch (same class of error as rate limiter the day before). Decorator wrapping concept still not understood. Property name mismatch is now a confirmed recurring habit across 3 answers on 2 consecutive papers. |

## Current Read (Updated April 3, 2026)

The student is no longer in a "blank beginner" state. The durable pattern now is:
- concept recognition and tracing improve faster than exact implementation,
- narrow remediation works,
- but transfer to fresh mixed prompts still breaks quickly,
- and the concept-code gap now shows up in new domains (refactoring, design patterns) exactly as it did in algorithms — confirming this is a learning-style pattern, not a topic-specific one.

Right now, the student is more reliable at:
- identifying the intended pattern,
- tracing code or traversal order,
- and explaining the broad idea,

than at:
- producing typo-free working code from scratch,
- handling exact method/property names and return behavior,
- and proving correctness on edge cases and complexity details.

## Stable Strengths

- Learns quickly after targeted remediation.
- Code tracing and output prediction are stronger than blank-page implementation.
- Event-loop ordering improved materially between March 14 and March 15 and now looks much more stable than before.
- Scope chain and lexical scoping basics are no longer the primary blocker.
- Tree traversal orders are reliable.
- Recursive tree structure is improving; `maxDepth` was mostly correct and the base-case idea is understood.
- Pattern recognition is ahead of execution: the student often knows they need a hash map, two pointers, bounds, or a queue even when the final code breaks.
- BST split-point reasoning and simple XOR-based missing-number work are now becoming more dependable than before.

## Improving But Not Yet Reliable

- Balanced vs unbalanced BST complexity is closer to stable but still needs exact wording under pressure.
- The min/max-bound idea for `isValidBST` is understood, but exact implementation still slips on naming, bound propagation, or examples.
- Monotonic-stack thinking is improving, but trace accuracy is not automatic yet.
- Hash-map, top-k, and heap selection are visible at the concept level, but fresh Day 13 implementations are not ready.
- Attention to detail is better than in the earliest tests, but it still collapses on broader fresh papers.
- Rolling-DP structure is improving, but explanation quality still lags behind the code shape.

## New Signals (April 3 — two sessions)

- **Factory Method structure transferred in one session.** After being entirely blank on April 3 morning, the candidate produced a mostly-correct Factory Method skeleton in the afternoon gate. This is the fastest single-session improvement recorded and confirms that the focused drill approach works for this student.
- **Property name mismatch is now a confirmed recurring habit.** Appeared in 3 answers across 2 consecutive papers: rate limiter (`this.user` vs `this.users`), Observer (`this.observer` vs `this.observers`), constructor param (`maxCalls` stored as `maxRequests`). Not a typo — a systematic failure to cross-check declaration against usage. One coaching fix: after writing a constructor, scan all property usages before writing anything else.
- **Copy-paste without adaptation.** Q3 Observer used `obs.update(this.symbol, this.price)` — directly lifted from the StockTracker focus session example without adapting to the new scenario. Signals shallow transfer: the structure is copied but the meaning of each line is not yet owned.
- **Decorator wrapping concept is the current hardest gap.** The candidate still conflates "wrapping an instance" with "extending a class." Specifically: `constructor(formatter)` → `this.formatter = formatter` → `this.formatter.format(text)` has not clicked. Every other pattern is at partial transfer; Decorator is still at near-zero for implementation.
- **System design concepts are a relative strength.** CAP theorem, caching, vertical vs horizontal scaling were all answered with real understanding. This is the most reliable new domain so far.

## Recurring Failure Modes

- Implementation precision under pressure is the main blocker.
  Common pattern: wrong property names, wrong method calls, missing `return`, inverted comparisons, syntax slips, or one typo that breaks an otherwise correct idea.
- Transfer is weaker than recovery.
  The student can improve meaningfully on a narrow retest, then drop sharply when the same ideas appear inside a broader fresh paper.
- Edge-case discipline is still inconsistent.
  Empty inputs, boundary conditions, base cases, and exact queue / BST behavior are not being checked reliably before submission.
- Complexity explanations are thinner than the final label.
  The student often writes `O(n)` or `O(log n)` without the supporting reason, and sometimes misses the `O(h)` vs worst-case `O(n)` distinction.
- Blank or near-blank answers are still costly.
  This happened in earlier evaluations, reappeared as skipped Day 13 work, and appeared again on the March 30 cumulative paper with a blank topological-sort answer; the student needs an "always attempt" rule.

## Historical Signals Worth Remembering

- Closure-heavy implementation was a major early weakness: module pattern, currying, memoization wrappers, and private-state utilities.
- Python reference / copy behavior was weak in the early assessments.
- These are not the current top blockers, but they remain good candidates for future spaced review because the underlying "concept known, implementation shaky" pattern still matches the student's profile.

## Coaching Notes That Actually Help

- Ask for the approach before the code.
- Make the student say the invariant or rule out loud: what stays true after each loop, recursive call, or transfer step.
- Require three checks before submission: one normal case, one smallest edge case, and one tricky boundary case.
- For data-structure questions, make the student read exact property names, method calls, and return values line by line before finalizing.
- Use narrow recovery blocks when a topic fails, but do not count the topic as consolidated until it also works on a fresh prompt.
- Ban blanks. A partial attempt is better than no evidence.

## Current Advancement Guardrails

Do not widen scope just because one recovery session looked better.

Before treating Day 11-13 carry-over as cleared, the student should be able to produce from memory:
1. A correct fresh stack / queue implementation with exact property names and return behavior.
2. A typo-free BST insert / validate solution with real counterexamples and correct bounds.
3. A real binary-search-on-answer solution, not a single-pass substitute.
4. A non-blank attempt at bucket-based top-k or equivalent required pattern work.

## Bottom Line

This student is improving, and the improvement is real. The durable lesson from the repo is not "the student does not understand the material"; it is "the student usually understands more than the submitted code proves."

Future teaching should optimize for transfer:
- explanation first,
- exact implementation second,
- edge-case checking third,
- and fresh verification after remediation before moving on.
