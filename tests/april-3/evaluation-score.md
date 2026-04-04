# APRIL 3 EVALUATION | DAY 20 + REFACTORING & DESIGN PATTERNS
**Date:** April 3, 2026
**Total Score: 37 / 100 (37%)**
**Recommendation: Do not advance to Phase 4. One targeted focus session required before moving on.**

---

## Section-by-Section Breakdown

| Section | Topic | Max | Scored | % |
|---|---|---:|---:|---:|
| A — Q1 | Identify Code Smells | 10 | 7.5 | 75% |
| A — Q2a | Extract Method | 5 | 3 | 60% |
| A — Q2b | Replace Temp with Query | 5 | 2.5 | 50% |
| A — Q2c | Replace Type Code with Polymorphism | 10 | 4 | 40% |
| A — Q3 | Technical Debt | 10 | 4 | 40% |
| **Section A Total** | | **40** | **21** | **52%** |
| B — Q4 | Pattern Classification | 10 | 4.5 | 45% |
| B — Q5 | Factory Method (implementation) | 12 | 0 | 0% |
| B — Q6 | Decorator + Observer (implementation) | 13 | 0 | 0% |
| **Section B Total** | | **35** | **4.5** | **13%** |
| C — Q7 | Rate Limiter (implementation) | 12 | 2.5 | 21% |
| C — Q8 | System Design Concepts | 13 | 8.5 | 65% |
| **Section C Total** | | **25** | **11** | **44%** |
| **Grand Total** | | **100** | **37** | **37%** |

---

## Question-Level Comments

### Q1 — Identify the Code Smell (7.5/10)

**What worked:**
- Snippet B (Message Chains / Coupler): category and smell name correct.
- Snippet C (Large Class / Bloater): correct.
- Snippet D (Switch Statements in a type-check function): correct category and smell, and the explanation correctly identified that every new shape requires editing the function — this was the best answer in the section.

**What broke:**
- Snippet A: Named "Abuser" and "Switch Statements" which is acceptable, but the explanation only said "too much if statements make it harder to understand". The real problem is that the type code has no semantic meaning and the logic cannot be extended without modification. Thin reasoning.
- Snippet E: Category "Change Preventer" was correct. But the specific smell named was "Divergent Change" — that is wrong. The correct smell is **Shotgun Surgery** (one change → many files). Divergent Change is the opposite (one class changes for many reasons). This is a terminology confusion that needs fixing.

---

### Q2a — Extract Method (3/5)

**What worked:** The refactored code is correct. Three functions were correctly extracted (`printHeader`, `printItemsAndCalculateTotal`, `printFooter`). The code is working and logically clean.

**What broke:** The question asked to name the **technique**. The candidate named the smell ("Long Method / Bloater") instead of the technique ("Extract Method"). This confusion between smell-naming and technique-naming appears in every Q2 answer and is the single biggest pattern to fix in Section A.

---

### Q2b — Replace Temp with Query (2.5/5)

**What worked:** The code is correct. `basePrice` was correctly extracted as a helper function and the original temp variable was removed. The trade-off answer showed partial understanding ("computing values complicated or changes in between").

**What broke:**
- Technique name: "Inline Class" is completely wrong. The correct name is "Replace Temp with Query." "Inline Class" is a technique for collapsing a class into another — an entirely different operation.
- Trade-off explanation was grammatically unclear and did not precisely state the performance concern (repeated computation of an expensive function).

---

### Q2c — Replace Type Code with Polymorphism (4/10)

**What worked:** The subclass structure is correct for Engineer and Manager. `getBonus()` and `getTitle()` are overridden cleanly.

**What broke:**
- **Intern subclass is missing.** The original had three types; only two were handled.
- **No factory function.** Without a factory, client code must still say `new Engineer(name)` — that puts the type decision back in the caller, which was the exact problem being solved.
- Technique named: "OO Abuser / Switch Statements" — again, this is the smell, not the technique. The required technique name is "Replace Type Code with Subclasses."
- No explanation of why this approach is better.

---

### Q3 — Technical Debt (4/10)

**Part A (2.5/4):** The loan analogy for technical debt is good and the deliberate vs inadvertent distinction was correct. But the question explicitly asked for "a concrete example of each" and none were given. The answer stayed at the definition level.

**Part B (1/3):** Correctly identified Magic Numbers as one smell. The second smell (the TODO comment as a Lazy Comment / Dispensable) was not mentioned. No refactoring technique was named for either smell — just identified the category.

**Part C (0.5/3):** The answer said Change Preventers "make the cost of future features really high" which is directionally correct. But the question asked to name two specific Change Preventer smells and explain how each one makes changes harder. Neither smell was named.

---

### Q4 — Pattern Classification (4.5/10)

- **Singleton (1.5/2):** Category correct, problem correct in substance, but no participants named.
- **Adapter (1/2):** Category correct, problem explanation was vague ("translation between instances"), no participants.
- **Observer (0/2):** The candidate listed "Observer" with no category, no problem, no participants. This is the pattern that appears most directly in Q6b, which was also left blank.
- **Factory Method (1/2):** Category correct, problem partially described, no participants.
- **Decorator (1/2):** Category correct, problem correct in spirit, no participants.

Pattern: the candidate knows categories but skips the participant roles entirely in every answer.

---

### Q5 — Factory Method Implementation (0/12): **BLANK**

This was the most important implementation question in Section B and it was not attempted. This directly confirms the candidate's own feedback: "learned the terms but when writing from scratch it's hard."

---

### Q6 — Decorator + Observer Implementation (0/13): **BLANK**

Both implementation questions in Q6 were skipped. These required the same patterns the candidate described in Q4. This is the largest single mark loss on the paper: 25 marks combined from Q5 and Q6 with nothing scored.

---

### Q7 — Rate Limiter (2.5/12)

The candidate understood that timestamps should be stored per user. That is correct at the concept level. The code has five critical bugs:

1. `this.user = []` declared in constructor but accessed as `this.users[userId]` — property name mismatch, code throws immediately.
2. Used an array instead of a `Map` — array index access on string userIds is broken.
3. No timestamp pruning — timestamps outside the window are never removed, which means the rate limit never resets.
4. No check against `maxRequests` — the function never actually blocks any request.
5. `allow()` does not return `true` or `false`. `Return user;` is outside the method body, is a syntax error, and references the wrong variable.

Complexity labels O(N) and O(N) are correct but the justification was wrong ("since it moves to constructor and set with just user as array" does not explain why either is O(N)).

High traffic answer ("increase horizontal scaling") shows awareness of distributed systems but missed the specific weakness of the timestamp approach (memory overhead) and the specific alternative (token bucket or fixed-window counter).

---

### Q8 — System Design Concepts (8.5/13)

**CAP (2/4):** All three properties correctly defined. Each pair's trade-off correctly described. Missing: no real database named for any pair — HBase, Cassandra, and PostgreSQL were all absent. "Partial tolerance" used instead of "partition tolerance" throughout.

**Caching (1.5/3):** Cache-aside correctly defined. Cache miss behavior correctly described. The third sub-question ("when would you NOT want caching?") was not answered at all.

**Scalability (3/3):** Both definitions correct, both scenarios given and appropriate. Full marks.

**SQL vs NoSQL (2/3):** Both positions correctly stated (ACID + joins for SQL, horizontal scale + flexible schema for NoSQL). Not structured as two distinct situations each with individual justification, so partial credit only.

---

## Summary of Strengths

- **Smell identification from code is reliable.** The candidate can read a snippet and correctly name the catalog category and specific smell in most cases. This is genuine vocabulary transfer.
- **Conceptual understanding of system design is solid.** CAP, caching, vertical vs horizontal scaling were all answered with real understanding, not just keyword recitation.
- **Refactoring code (when attempted) is structurally correct.** Q2a and Q2b produced working implementations even if the technique names were wrong.
- **Subclass inheritance structure is understood.** Q2c produced a correct class hierarchy (minus Intern) without scaffolding.

## Summary of Weaknesses

1. **Smell name vs technique name confusion.** Every Q2 answer named the smell or category when the question asked for the technique. "Long Method" ≠ "Extract Method." "Switch Statements" ≠ "Replace Type Code with Subclasses." This is a consistent pattern, not a one-time slip.
2. **Pattern implementation is the wall.** Q5 and Q6 were entirely blank. 25 marks lost. The candidate knows what Factory Method, Observer, and Decorator do but cannot produce working code for any of them under test conditions.
3. **Rate limiter has five structural bugs.** The approach was correct but translation to code broke at every step: wrong property names, wrong data structure, missing pruning, missing guard, missing return.
4. **Participant roles never named.** In Q4, every pattern answer skipped the "key participants" sub-question. This means the candidate understands the pattern's purpose but not its structure.
5. **Concrete examples missing in explanation answers.** Q3a (no code examples for debt types) and Q8a (no database names for CAP pairs) both lost marks on sub-questions that explicitly asked for concrete examples.

## Candidate Feedback Alignment

The candidate reported: *"Wasn't able to complete the code within 1 hour. Main issue I felt is I learned the terms in refactoring but when writing from scratch it's hard."*

This matches the evidence exactly:
- Section A (mostly naming / reading code): 52%
- Section B (mostly writing code from scratch): 13%
- Section C (mixed concepts + broken implementation): 44%

The gap between vocabulary and implementation is the same pattern that has appeared across every assessment in this repo. It is now showing up in a new domain (refactoring + design patterns), which means it is a learning style issue, not a topic-specific issue.

## Recommendation

**Do not advance to Phase 4 (Web Dev / Day 21).**

One focused implementation session is required before moving on. The session must close these three gaps:
1. Distinguish technique name from smell name — drill with flashcard-style prompts
2. Implement Factory Method, Observer, and Decorator from a blank page with no scaffold
3. Fix the five rate limiter bugs with explanation of each fix

After that session, a short verification gate (not a full paper) will determine readiness to move to Day 21.
