# Workflow Reference

## Canonical Files

- `agent.md`: repo-local operating guide for test creation, scoring, carry-over logic, and naming conventions.
- `plan.md`: source of truth for the learning day, phase, and carry-over rules.
- `tests/<date>/question-paper.md`: the day’s assessment prompt.
- `tests/<date>/answer-key.md` or `answer-sheet.md`: authoritative answers and scoring guide.
- `tests/<date>/candidate-answers.md`: the student's real submitted answers or a faithful transcription after submission.
- `tests/<date>/evaluation-score.md`: preferred scored breakdown and remediation note filename for post-submission work.
- `tests/<date>/focus-session.md`: targeted practice after a failed or weak assessment.
- `progress-card.md`: long-term memory of strengths, weaknesses, and trend.

## Reusable Checklist

1. Read `plan.md` and `agent.md`, then locate the intended day or phase.
1. Scan the latest scored tests and the progress card for repeat weaknesses.
1. Decide whether the new item is a fresh day, a carry-over day, or a remediation day.
1. If it is a fresh day, create only the paper and teacher answer file by default.
1. If it is a completed day, save the student's answers first, then score them.
1. Match the question style to the evidence:
   - concept misunderstanding -> tracing or explanation question
   - implementation gap -> write-code question
   - edge-case miss -> trap question with an explicit boundary
   - repeated blank answers -> mandatory attempt question
1. Draft the paper, then the answer key. Only after submission create scoring notes.
1. If the student is stuck, add a focus session with only the weakest topic.
1. After scoring, update `plan.md` if the next step changes.
1. Update the progress card with concise, durable memory only when the new result changes the long-term picture.

## Test Design Heuristics

- One file can cover multiple topics, but each section should have a clear purpose.
- Use a mix of tracing, implementation, and explanation when a topic matters for interviews.
- Keep the hardest questions tied to the student's actual misses.
- Do not overfit to a single previous answer; prefer patterns that test the same concept from a different angle.
- When updating a previous day, preserve the original evidence trail and add the new judgment beside it.

## Score Interpretation

- `90-100`: ready to advance.
- `80-89`: mostly solid, minor review only.
- `70-79`: acceptable, but watch the known weak spots.
- `<70`: repeat or remediate before moving on.

## Template Language

- "Strengths demonstrated" should describe observable behavior.
- "Areas for growth" should name the exact skill gap.
- "Next action" should be explicit and short.
- "Evidence used" should cite the dated files that actually contained student work.
