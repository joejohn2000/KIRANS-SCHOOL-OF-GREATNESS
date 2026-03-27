# Test Authoring Agent Guide

Use this file when creating or updating tests, answer keys, evaluations, remediation notes, and progress tracking in this repo.

The goal is to keep all future work aligned with:
- the mastery path in `plan.md`,
- the student's actual performance evidence in `tests/`,
- and the long-term memory in `progress-card.md`.

## What This Repo Is

This repo is not just a collection of test papers. It is a teaching loop:
1. plan the next skill target,
2. test it,
3. evaluate the answers,
4. identify gaps,
5. adjust the next day,
6. update student memory.

Every new test should fit that loop.

## Canonical Files

Read these first before creating anything new:
- `plan.md`
- `progress-card.md`
- latest scored evaluation file in `tests/`
- latest candidate answer file in `tests/`
- latest relevant answer key / answer sheet in `tests/`

Important:
- Do not assume calendar date equals plan day number.
- As of March 27, 2026, the repo evidence shows real assessed progress through the early algorithms/data-structures stretch, with carry-over gaps still active. Use evidence first, calendar second.

## Primary Rule

Always base the next test on both:
- the intended direction in `plan.md`
- the student's most recent demonstrated strengths and weaknesses

If those conflict, prefer the evidence and adapt the plan instead of blindly advancing.

## Standard Workflow

### 1. Determine the current teaching state

Before drafting a new test:
- read the relevant day in `plan.md`
- read the `Daily Adjustment Log` at the bottom of `plan.md`
- inspect the latest scored evaluation
- inspect the latest student submission
- inspect `progress-card.md`

Then answer:
- What was the intended topic?
- What did the student actually master?
- What carry-over weaknesses are still active?
- Should the next test be advance, review, or catch-up?

### 2. Choose the test mode

Use one of these modes:

- `Foundations review`
  Best for early topics, mixed concept + implementation, moderate scaffolding.

- `Tricky focus`
  Best when the student knows the concepts but misses details, edge cases, or tracing order.

- `Debug & solve`
  Best when the student needs deeper implementation accuracy, bug-finding, and complexity justification.

- `Catch-up / remediation`
  Best after repeated failure, blanks, or major confusion. Narrow scope. No new topic unless the user explicitly wants it.

- `Verification gate only`
  Best for a short day or plan checkpoint. Usually 1 coding problem + 1 explanation prompt.

### 3. Decide whether to advance

Default decision rules unless the user overrides:
- If the latest result is clearly below pass level or shows major blanks, repeat the weak topic and add remediation.
- If the student is around the satisfactory band, advance carefully but include carry-over questions.
- If the student is clearly strong, advance and keep only light carry-over.

Repo-informed heuristic:
- `< 70%` or major unanswered sections: do not fully advance.
- `70-84%`: advance carefully with carry-over.
- `85%+`: advance with light review only.

Also apply the plan rules:
- fail one gate: add carry-over next day
- fail two consecutive days: next day becomes catch-up
- from adapted later phases: no blanks, explanation-first, complexity justification mandatory

## File and Folder Conventions

Create one dated folder per test session:
- `tests/march-27/`
- if there is a second session the same day: `tests/march-27-2nd/`
- if there is a third: `tests/march-27-3rd/`

Preferred file set for a full lifecycle:
- `question-paper.md`
- `answer-key.md` or `answer-sheet.md`
- `candidate-answers.md`
- `evaluation-score.md`
- `focus-session.md` if remediation is needed

Use these naming conventions going forward:
- prefer hyphen-case, not underscores
- prefer `answer-key.md` for direct answer keys
- prefer `answer-sheet.md` for longer model solutions or debug-style worked answers
- prefer `evaluation-score.md` for final scoring reports

Backwards compatibility:
- older folders already mix `answer_key.md`, `evaluation_scoring.md`, and similar names
- do not rename old files unless explicitly asked

## What to Create for Each Task

### If the user asks to create a new test

Create at least:
- `question-paper.md`
- `answer-key.md` or `answer-sheet.md`

Do not create by default:
- `candidate-answers.md`
- `evaluation-score.md`

Those belong to the post-submission stage, after the student has actually answered.

Only create a blank response scaffold if the user explicitly asks for one.

### If the user asks to score a completed test

Create:
- `candidate-answers.md` if the student answers are being stored in the repo and the file does not already exist
- `evaluation-score.md`

And usually update:
- `focus-session.md` if there are repeatable weakness patterns
- `plan.md` if the daily adjustment or carry-over should change
- `progress-card.md` if the result materially changes the student memory

Preferred repo-local skill for this stage:
- `.codex/skills/student-result-evaluator`

Recommended post-submission order:
1. Save the student's actual answers into `candidate-answers.md`
2. Create `evaluation-score.md`
3. Create `focus-session.md` if needed
4. Update `plan.md`
5. Update `progress-card.md`

### If the user asks for remediation only

Create:
- `focus-session.md`

Optionally add:
- a short mini-test or gate inside the same dated folder

## Question Paper Design Rules

Every question paper should include:
- title
- date
- focus/topics
- total marks
- time allowed
- short instructions
- clear section structure

Match the question style to the learning stage:

- Early foundations:
  use multiple choice, short answers, code prediction, and small implementation prompts.

- Mid-stage algorithms:
  use bug tracing, edge cases, corrected implementations, and complexity reasoning.

- Later practice days:
  use fewer but deeper LeetCode-style questions and written explanation gates.

### Difficulty tuning

Tune difficulty using the student's actual pattern:
- If tracing is stronger than coding, include more implementation repair and fewer pure theory questions.
- If syntax mistakes are frequent, require sample-case verification and edge-case checks.
- If blanks are recurring, prefer narrower scope and explicit attempt instructions.
- If explanations are weak, require approach and complexity justification before code.

### Marks guidance

Default total: `100`

Useful section patterns:
- `20-30` marks for concept or tracing
- `30-40` marks for implementation
- `20-30` marks for debugging or edge cases
- `10-20` marks for explanation / complexity justification

For later-stage harder papers, fewer questions with deeper marks are better than many shallow questions.

## Answer Key / Answer Sheet Rules

Always create the answer file alongside the question paper unless the user explicitly says draft-only.

The answer file should:
- give the correct answer
- explain why
- include corrected code where relevant
- include time/space complexity where the paper asks for it
- be strict about the exact bug, not just the symptom

Use:
- `answer-key.md` for shorter direct answers
- `answer-sheet.md` for worked solutions, detailed traces, or debug-heavy papers

## Candidate Answers File

Create `candidate-answers.md` only after the student has actually answered, unless the user explicitly asks for a blank scaffold.

Default meaning of `candidate-answers.md` in this repo:
- the student's real submitted answers
- or a faithful transcription of answers provided in chat / terminal

Do not use `candidate-answers.md` as a default placeholder file during initial test creation.

Use a lightweight structure:
- title
- date
- numbered placeholders matching each question

Do not add hints or model answers to the candidate file.

## Evaluation Rules

The evaluation file should not just score answers. It should diagnose the learning pattern.

Every `evaluation-score.md` should contain:
- total score
- section-by-section marks
- question-level comments
- summary of strengths
- summary of weaknesses
- explicit recommendation: advance, advance-with-carry-over, or repeat/catch-up

When scoring:
- give credit for correct reasoning even if wording is imperfect
- deduct heavily for broken implementation when the question required working code
- do not reward blanks
- note when the student got the output right but the explanation wrong
- note when the student understood the concept but failed on implementation precision

Post-evaluation follow-through:
- update `plan.md` when the result changes the next day's direction, carry-over, or catch-up logic
- update `progress-card.md` when the result changes the durable memory of strengths, weaknesses, or trend
- create `focus-session.md` when the weakness pattern needs targeted remediation rather than just a score note

## Focus Session Rules

Create `focus-session.md` when:
- the student fails a day
- the same weakness appears across multiple dates
- the student leaves blanks
- the gap is pattern-based, not one isolated mistake

A good focus session should include:
- what was passed and can be skipped
- what failed and why it matters
- 2-5 very targeted drills
- a verification gate for that weak area

Keep it narrow. One strong remediation note is better than a generic study dump.

## Progress Card Rules

`progress-card.md` is the long-term memory.

Update it only when there is a meaningful new signal:
- a clear improvement trend
- a repeated weakness becoming stable
- a major shift in level
- a new consistent behavior under pressure

Do not rewrite the whole card for a tiny change.

When updating the card, prefer:
- stable patterns
- evidence-backed strengths
- repeated weaknesses
- coaching notes that help future test design

## How to Tweak `plan.md`

Only tweak `plan.md` when the evidence justifies it.

Safe updates:
- add a carry-over note
- mark a gate result
- clarify that a planned day became catch-up
- add adapted emphasis based on repeated evidence

Avoid:
- silently jumping the student ahead
- rewriting whole phases without evidence
- changing day intent just because of the calendar

## Style Rules for This Repo

Keep the tone:
- direct
- challenging but supportive
- evidence-based
- specific about failure modes

Good phrasing:
- "The student understands the concept but loses marks on implementation precision."
- "Do not advance yet."
- "This is improving, but still unstable under pressure."

Avoid vague comments like:
- "Needs work"
- "Study more"
- "Practice harder"

## Current Evidence Summary for Future Agents

These patterns are already established in the repo:
- conceptual understanding has improved faster than implementation accuracy
- tracing code is stronger than writing correct code from scratch
- closure-heavy implementation has been a recurring weakness
- event-loop understanding improved after remediation
- edge cases and exactness still need reinforcement
- complexity justification is often thinner than the final complexity label

Use those as defaults unless newer evidence clearly replaces them.

## Default Checklist Before Finishing

Before you finish a test-related task, verify:
- Is the work aligned with the right plan day or adapted carry-over?
- Did you use the latest evidence, not just the plan?
- Did you create the matching answer file?
- Are filenames consistent with repo conventions?
- If scoring was involved, did you record an explicit next-step recommendation?
- If this was a pre-submission test creation task, did you avoid creating `candidate-answers.md` and `evaluation-score.md` by default?
- If this was a post-submission scoring task, did you update `plan.md` and `progress-card.md` where justified?
- If the result changes the student memory, did you update `progress-card.md`?

## Suggested March 27 Starting Point

If asked to build the March 27, 2026 test and no other override is given:
- do not assume "March 27" means "Day 27" in the plan
- first inspect the latest completed evidence and carry-over state
- prefer a test that bridges current assessed algorithm/data-structure progress with remaining implementation gaps
- include at least one explanation-first question and one implementation-precision question

If there is uncertainty, choose evidence-aligned progression over calendar-aligned progression.
