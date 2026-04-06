# APRIL 3 FOCUS GATE — EVALUATION
**Date:** April 3, 2026
**Total Score: 23 / 50 (46%)**
**Gate threshold: 38 / 50 (76%)**
**Result: GATE NOT PASSED — targeted carry-over applied, advance to Day 21 regardless**

---

## Score Breakdown

| Question | Max | Scored | % |
|---|---|---:|---:|
| Q1a — Long Method → Extract Method | 2 | 2 | 100% |
| Q1b — Magic Number → symbolic constant | 2 | 1.5 | 75% |
| Q1c — Switch Statements → Replace Type Code | 2 | 1 | 50% |
| Q1d — Divergent Change → Extract Class | 2 | 0 | 0% |
| **Q1 Total** | **8** | **4.5** | **56%** |
| Q2 — Factory Method | 15 | 9 | 60% |
| Q3 — Observer | 12 | 6 | 50% |
| Q4 — Decorator | 15 | 2 | 13% |
| Q5 — Rate Limiter (bonus) | 8 | 1.5 | — |
| **Grand Total** | **50** | **23** | **46%** |

---

## Question-Level Comments

### Q1 — Smell → Technique (4.5 / 8)

**Q1a (2/2):** Correct. "Extract Method" named precisely. Explanation correct in substance. Full marks.

**Q1b (1.5/2):** Technique named as "Replace Magic Number with constant" — close, but the exact catalog name is "Replace Magic Number with **Symbolic** Constant." One word away. The explanation is correct. Half a mark deducted for imprecise technique name on a question that specifically tests technique naming.

**Q1c (1/2):** The idea is right — "Replace with polymorphism" shows the student knows what needs to happen. But "Replace with polymorphism" is not the exact technique name. The correct name is "Replace Type Code with Subclasses" (or "Replace Conditional with Polymorphism" for a different but related technique). The explanation correctly identifies the solution. Half marks for correct idea, half deducted for imprecise name.

**Q1d (0/2):** Same error as the original April 3 paper. The answer is "Extract Method" — which is wrong. The correct technique for Divergent Change is **Extract Class**. Extract Method produces functions; Extract Class produces a new class with its own responsibility. The explanation ("different responsibilities are broken down to separate functions") also describes Extract Method, not Extract Class. This is the only Q1 error that has not improved at all between the two papers.

---

### Q2 — Factory Method (9 / 15)

**What worked — and this is the biggest improvement on this paper:**
The overall structure is present and correct. Base class, three concrete subclasses extending it, a static factory with a `create()` method and a `throw` for unknown types, a usage example. Yesterday this was entirely blank. Today the full skeleton is here. This is real transfer.

Participant identification: "PaymentMethodFactory and PaymentMethod are the two participants" — correct. ✓

Open/Closed Principle: "Without modifying base logic and client logic it can create crypto payment methods so it follows open/close principle" — correct idea, poorly expressed but the reasoning is sound. ✓

**What broke:**
1. `Class` with a capital C for all three concrete classes — JavaScript is case-sensitive. `Class` is not a keyword; `class` is. All three concrete classes would throw `ReferenceError`. This is a precision slip, not a concept failure.
2. Mixed quotes in all three `pay()` methods: `"amount charged $${amount}\`` — starts with a double quote, ends with a backtick. This is a syntax error. Template literals require backtick on both sides.
3. Factory class named `PaymentMethodFactory` in the definition but called as `PaymentFactory` in the usage — reference error.
4. Usage example calls `PaymentFactory.create(type)` where `type` is undefined — `type` was never declared.
5. Variable names shadow the class names (`let CreditCard = ...`) — this creates a scoping conflict and defeats the purpose of the factory; the client is still spelling out all three types explicitly.

Score: 9/15 (4 code quality, 3 participants, 2 OCP)

---

### Q3 — Observer (6 / 12)

**What worked:**
- `subscribe()` and `unsubscribe()` logic is correct — the filter pattern is right.
- `PhoneDisplay` and `WebDashboard` have the correct `update(temp)` implementations.
- Explanation: "WeatherStation depends on a common interface allowing it to notify any observer without any specific internal logic or implementation" — this is correct and well-put. ✓

**What broke — the critical bug:**
`this.observer = []` in the constructor, but `this.observers` is used in every other method. This is the exact same property name mismatch error as the rate limiter yesterday (`this.user` vs `this.users`). The code would crash immediately on `subscribe()` because `this.observers` does not exist.

This error pattern has now appeared twice across two consecutive tests. It is not a typo — it is a habit of not checking that the property name you declare matches the property name you use.

**Second bug:**
`obs.update(this.symbol, this.price)` inside `setTemperature` — these are `StockTracker` properties from the focus session example. The candidate copied the notify loop from the drill without adapting it to the new scenario. `WeatherStation` has no `this.symbol` or `this.price`. The correct call is `obs.update(temp)`.

No usage example or output trace was provided (a required part of the question).

Score: 6/12 (3 code, 3 explanation)

---

### Q4 — Decorator (2 / 15)

This is the most broken answer on the paper. The concept has not transferred.

**The specific failure — wrapping vs extending:**

The candidate wrote:
```javascript
class TextFormatterDecorator extends TextFormatter {
  constructor(text) {
    this.text = text;
  }
```

Two fundamental errors here:
1. The decorator should **hold a reference** to another formatter — `constructor(formatter) { this.formatter = formatter }`. Instead, the constructor takes a string `text` and stores it as `this.text`. The decorator cannot delegate to anything because it holds a string, not a formatter instance.
2. `extends TextFormatter` is wrong for the base decorator wrapper. The wrapper should have its own identity; extending the concrete base muddies the inheritance and breaks the wrapping contract.

`UpperCaseFormatter` is nested inside `TextFormatterDecorator`'s class body — JavaScript does not support class declarations inside a class body. This is a syntax error.

`ExclamationFormatter` is referenced in the usage example but never defined anywhere in the answer.

The call trace (worth 5 marks) was not provided.

The explanation of why Decorator beats subclassing (worth 2 marks) was not provided.

What is correct: `TextFormatter` base class is fine. `UpperCaseFormatter` applies `.toUpperCase()` — the right transformation. The stacked usage example is written. The idea is present; the structure is broken.

Score: 2/15 (2 for base class + correct transformation idea)

---

### Q5 — Rate Limiter / Bonus (1.5 / 8)

**Genuine improvement from yesterday:**
`this.timestamps = new Map()` — correct data structure, correct property name. This is a direct fix of the most fundamental bug from the April 3 paper. The candidate learned this.

**What is still broken:**
```javascript
this.maxRequests = maxRequests;  // 'maxRequests' is undefined — parameter is 'maxCalls'
```
Constructor parameter is `maxCalls` but stored using the undeclared name `maxRequests`. Same class of error as the property mismatch in Q3.

Inside `isAllowed`:
- `userTimestamps` is never declared
- `now` is never declared
- No IP address lookup from the Map (`timestamps.get(ipAddress)`)
- No window calculation (`Date.now() - this.windowMs`)
- No pruning
- No `return false`

No complexity answer. No bug identification from the previous submission.

Score: 1.5/8 (1.5 for the Map improvement and guard shape)

---

## Pattern Analysis

Three signals worth naming separately from the individual question scores:

**Signal 1 — Real structural improvement in Q2**
Factory Method went from 0/12 (entirely blank yesterday) to a mostly correct structure with syntax-level bugs today. The four-part shape (base class, concrete classes, factory, usage) was reproduced. This is the clearest evidence that the focus session worked for Factory Method. The bugs that remain are precision errors, not concept failures.

**Signal 2 — Property name mismatch is now a documented recurring bug**
This error has appeared in three answers across two consecutive papers:
- April 3: rate limiter — `this.user` declared, `this.users` accessed
- April 3-2nd: Observer — `this.observer` declared, `this.observers` accessed
- April 3-2nd: rate limiter — `this.maxRequests = maxRequests` (wrong parameter name)

This is a habit, not a coincidence. The candidate writes the declaration and the usage in different sessions (or mental contexts) without checking they match. One practice rule will fix this: after writing the constructor, read back every property name against every place it is used before writing anything else.

**Signal 3 — Copy-paste without adaptation**
`obs.update(this.symbol, this.price)` in Q3 is directly copied from the StockTracker focus session example. The candidate translated the Observer shape but did not adapt the method call to the new scenario. This shows the transfer is shallow — the structure is copied, but the meaning of each line is not fully understood yet.

---

## Recommendation

**Do not run a third full test on these topics.**

The gate was not passed (23/50 vs 38/50) but the direction is clearly positive:
- Q1 improved from 7.5/10 → 4.5/8 (proportionally similar, with one persistent error)
- Q2 improved from 0/12 → 9/15 (major structural transfer happened)
- Q3/Q4 still broken, but Q3 is closer than Q4
- Q5 shows one genuine improvement (Map) with incomplete follow-through

Running another 60-minute gate test on these patterns would delay the main plan without enough marginal benefit. The remaining gaps are better addressed as daily carry-over exercises woven into Days 21 onwards, not as blocking tests.

**Specific carry-over for Day 21:**

1. **5-minute fix before Day 21 starts:** Q1d — Divergent Change → Extract Class. Write the difference between Extract Method (produces a function) and Extract Class (produces a new class with its own responsibility) in one sentence. No code needed. One minute.

2. **Drill rule (every session, not just today):** After writing a constructor, immediately read back every property name in the class body and confirm each one matches exactly what was declared. This kills the mismatch bug at the source.

3. **Decorator carry-over:** Before Day 21's pattern drills, spend 15 minutes writing the `FormatterDecorator` constructor correctly from scratch — `constructor(formatter) { this.formatter = formatter }` — and call `this.formatter.format(text)` in a delegation method. The wrapping concept is the one thing that has not clicked yet.

**Advance to Day 21.** The focus session work is done. These gaps carry forward as active notes, not blocking conditions.
