---
name: student-result-evaluator
description: Evaluate a completed student test in this repo. Use when a user provides finished answers and wants `evaluation-score.md`, an updated `progress-card.md`, and an evidence-based update to the evolving `plan.md` based on the latest result.
---

# Student Result Evaluator

## Overview

Use this skill only for the post-submission stage.

Its job is to take:
- the completed student answers,
- the matching question paper,
- the matching answer key or answer sheet,
- the current `plan.md`,
- and the current `progress-card.md`,

and turn that into:
- `candidate-answers.md` if needed,
- `evaluation-score.md`,
- optional `focus-session.md`,
- an updated `plan.md`,
- and an updated `progress-card.md`.

## When To Use

Trigger this skill when the user asks to:
- evaluate a finished test
- score student answers
- update the student's progress memory after a test
- adapt the next plan based on the result
- optimize the evolving `plan.md` from new evidence

Do not use this skill for initial test creation. That belongs to the broader assessment workflow.

## Required Inputs

Read these before scoring:
1. `agent.md`
1. `plan.md`
1. `progress-card.md`
1. the relevant dated `question-paper.md`
1. the matching `answer-key.md` or `answer-sheet.md`
1. the student's real answers
1. the most recent prior scored evaluation, if one exists

If the student's answers are only in chat or terminal, save them into `candidate-answers.md` first.

## Scoring Workflow

1. Identify the exact dated test folder being scored.
1. Save the student's real answers into `candidate-answers.md` if that file does not yet exist.
1. Compare student answers against the teacher answer file question by question.
1. Create `evaluation-score.md` with marks, comments, strengths, weaknesses, and a next-step recommendation.
1. Decide whether a `focus-session.md` is needed.
1. Update `plan.md` only where the new evidence changes the next-day direction, carry-over, or catch-up logic.
1. Update `progress-card.md` only where the new evidence changes durable memory.

## Evaluation Rules

- Use real student work as evidence, not guesses.
- Give credit for correct reasoning even if wording is imperfect.
- Deduct when code is broken, incomplete, or misses required edge cases.
- Do not reward blanks.
- Explicitly note the pattern when the student:
  - knows the concept but cannot implement it
  - gets the output right but the explanation wrong
  - misses edge cases
  - improves meaningfully from prior attempts

## Plan Evolution Rules

Treat `plan.md` as a living document.

Safe updates:
- mark the gate result in the adjustment log
- add a carry-over note
- convert the next day into catch-up when repeated failure justifies it
- add adapted emphasis when the same weakness keeps recurring

Avoid:
- rewriting unrelated phases
- silently skipping ahead without evidence
- changing the plan because of calendar date alone

Prefer small, evidence-backed edits over large rewrites.

## Progress Card Rules

Update `progress-card.md` only with durable signals:
- score trend changes
- a weakness becomes clearly repeated
- a strength becomes stable
- a coaching note becomes consistently true

Do not rewrite the card for a small one-off mistake.

## Output Expectations

### `evaluation-score.md`

Must include:
- date
- test focus
- section totals
- question-level comments
- overall score
- strengths demonstrated
- areas for growth
- evidence-based notes
- explicit recommendation:
  - ready to advance
  - advance with carry-over
  - repeat a specific day/topic
  - catch-up/remediation day needed

### `plan.md`

Only update the parts justified by the new result:
- daily adjustment log
- carry-over wording
- next-day focus
- adapted notes

### `progress-card.md`

Write memory, not a transcript:
- preserve stable observations
- add only meaningful new evidence
- prefer pattern summaries over one-test narration

## Good Defaults

- Use concrete dates.
- Keep the tone direct, supportive, and evidence-based.
- If the test result is borderline, prefer `advance with carry-over` over pretending it is a clean pass.
- If the student left blanks or failed key implementation tasks, say so clearly.
- If the result materially changes the learning path, update both `plan.md` and `progress-card.md` in the same pass.

## Reference

See [evaluation reference](references/evaluation.md) for the post-submission checklist and plan-update heuristics.
