# Plan Optimization Design — 2026-03-12

## Context
30-day FAANG-targeted learning plan for a developer with:
- Known languages: Python, JavaScript (stronger), Kotlin (dropping per user preference)
- Demonstrated skills: var/let/const, Python list mutation, basic control flow (FizzBuzz)
- Known gaps: Big O complexity, hash table problem-solving, JS closure edge cases
- Time commitment: 5+ hours/day (confirmed)

## Design Decisions

### Languages
- JS and Python only
- No redundant multi-language exercises for topics already demonstrated

### Output Artifact
The plan is a **full 30-day upfront document** written into `plan.md`. It is updated dynamically after each day based on user-reported performance. The document is the single source of truth — not generated session-by-session.

### Day Format
Each day follows this structure:
1. **Objective** — single focused goal
2. **Learning block (2hrs)** — concept + examples in JS and Python
3. **Practice block (2hrs)** — 3–5 specific problems to solve (named explicitly)
4. **Review block (1hr)** — reflect, document, note what was hard
5. **Verification gate** — one coding challenge + one written explanation prompt
   - Pass both = move on to next day
   - Fail either = a carry-over task is prepended to the next day (max 1hr carry-over)
   - Consecutive failures (2+ days): flag to human, compress or swap next day's topic

### Big O Insertion
Big O complexity is a standalone half-day block placed at the **start of Day 3**, before any algorithm content begins. Days 1–2 remain foundations. Day 3 opens with 2hrs of Big O, then its normal content follows in the remaining 3hrs.

### Carry-Over Cap
- Max 1 carry-over task per day (1hr)
- If a user fails 2+ days consecutively, the next day is marked as a Catch-Up Day: repeat the weakest topic, no new content introduced
- The 30-day window is fixed — topics may be compressed or de-prioritized, not extended

### Dynamic Adjustment
After each day:
- User reports results (pass/fail on verification gate)
- The next day's content in `plan.md` is updated to reflect carry-overs or topic adjustments
- No changes are made to days already completed

## Phase & Topic Breakdown

| Phase | Days | Topics |
|-------|------|--------|
| 1 | 1–5 | Variables & types (quick review), Control flow (quick review + closure gaps), Big O intro, Functions & scope, Arrays/Lists |
| 2 | 6–12 | Dictionaries/Maps, Recursion, Sorting algorithms, Searching algorithms, Hash tables, Linked lists, Stacks & Queues |
| 3 | 13–20 | Trees & BST, Heaps, Graphs (representation + traversal), Graph algorithms, Dynamic programming, Strings & pattern matching, Bit manipulation, OOP |
| 4 | 21–25 | HTML5 & accessibility, CSS layouts, JS deep dive (closures/async/event loop), React fundamentals, Node.js & REST APIs |
| 5 | 26–30 | Algorithm practice sessions, System design practice, Full-stack project, Mock interview + gap review |

## Verification Gate Format (per day)

**Coding challenge**: A concrete problem the user must solve and submit (LeetCode-style or equivalent). Specific problem named in the plan.

**Written explanation**: A specific question the user must answer in 3–5 sentences. Tests conceptual understanding, not just coding ability.

Both gates are defined in advance in the plan — not generated on the fly.
