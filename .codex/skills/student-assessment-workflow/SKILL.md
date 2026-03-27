---
name: student-assessment-workflow
description: Create and update this repo's dated student assessment workflow files. For new test days, produce only the question paper and teacher answer key. After the student answers, create candidate answers, evaluation notes, remediation/focus sessions, plan updates, and progress-card updates based on plan.md and real evidence.
---

# Student Assessment Workflow

## Overview

Use this skill when working in `KIRANS-SCHOOL-OF-GREATNESS` to produce or revise the assessment workflow for a day.

Use a two-stage flow:
- pre-submission: create the question paper and teacher answer file
- post-submission: save the student's answers, score them, adjust the plan, and update long-term memory

## Workflow

1. Read `plan.md` first.
1. Read `agent.md` for the repo's current workflow rules and naming conventions.
1. Inspect the latest relevant test folders and the current `progress-card.md`.
1. Use only real student submissions or scored evaluations as evidence. Treat answer keys and question papers as curriculum context, not performance evidence.
1. Infer the next day or topic from the plan's phase ordering, carry-over notes, and the latest real evidence. Do not assume the calendar date matches the plan day number.
1. Create or update the dated assessment files with consistent naming and aligned difficulty.
1. Keep the tone direct, encouraging, and evidence-based.

## What To Produce

For a new test day, create only:

- `question-paper.md`
- `answer-key.md` or `answer-sheet.md`

After the student answers, create or update:

- `candidate-answers.md`
- `evaluation-score.md`
- `focus-session.md` or remediation notes when gaps persist
- `plan.md` when the next-day direction should change
- `progress-card.md` when the long-term memory should change

If you are updating a historical folder that already uses `answer_key.md` or `evaluation_scoring.md`, preserve the old filename unless the user asks to normalize it.

## Difficulty Rules

- Start from the current plan day unless evidence says the student should repeat or catch up.
- Increase difficulty only after the prior gate is clearly passed.
- If the student repeatedly misses a concept, repeat it with a different question shape rather than moving on.
- Prefer fewer topics with stronger verification over broad coverage with thin marking.
- Make edge cases explicit when a topic has shown past mistakes.

## Evidence Rules

- Use scored files and student submissions as primary evidence.
- Use notes like `progress-card-march-22.md` to summarize trend, not as a substitute for raw evidence.
- If a file only contains an answer key or a question paper, do not treat it as student performance.
- When a result is ambiguous, state the assumption in the generated file instead of silently inventing certainty.

## Writing Style

- Keep Markdown simple and readable.
- Use concrete dates.
- Make strengths and weaknesses specific.
- Prefer "what the student can do" and "what breaks" over vague praise or criticism.
- Keep explanations short enough that the next agent can scan them quickly.

## Output Order

When generating a fresh day, use this order:

1. Build the question paper from `plan.md`.
1. Draft the answer key or answer sheet.

When evaluating a completed day, use this order:

1. Save the student's actual answers into `candidate-answers.md` if needed.
1. Create `evaluation-score.md`.
1. Add a focus session or remediation note if the result is below target.
1. Update `plan.md` if the result changes carry-over or next-day scope.
1. Update `progress-card.md` if the result changes the durable memory of the student.

## Good Defaults

- File names should follow the dated folder pattern already used in `tests/`.
- Prefer hyphen-case names for new files.
- Keep all content ASCII unless the repo already uses non-ASCII in that file.
- If a day is a carry-over day, explicitly say what is being repeated and why.
- If a test is meant to verify plan progress, align questions to the current phase and the current weak spots.
- Do not create `candidate-answers.md` or `evaluation-score.md` during initial test generation unless the user explicitly asks for a scaffold.

## Reference

See [workflow reference](references/workflow.md) for the canonical file map and a reusable checklist.

For the dedicated post-submission scoring/update flow, prefer the repo-local `student-result-evaluator` skill.
