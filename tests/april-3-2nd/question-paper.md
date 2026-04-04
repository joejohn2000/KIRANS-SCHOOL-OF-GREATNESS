# APRIL 3 — FOCUS SESSION GATE TEST
**Date:** April 3, 2026
**Mode:** Verification gate — fresh prompts only, no scaffolding
**Focus:** Smell vs technique naming · Factory Method · Observer · Decorator · Rate Limiter
**Total Marks:** 50
**Time Allowed:** 60 minutes

---

> "Same pattern, different scenario. If it only works on the drill example, it hasn't transferred."

---

## Instructions

1. All code in JavaScript.
2. No blanks. A partial attempt scores more than nothing.
3. For every implementation question: write the class structure **first** (just the method signatures), then fill in the body. This prevents syntax errors from breaking an otherwise correct idea.
4. For Q1: name the **technique**, not the smell category. Those are different words.
5. Before submitting any method, trace it once with a real value in your head.

---

## Q1. Smell → Technique (8 marks)

For each snippet, you are given the smell name. Write the exact **refactoring technique** that fixes it. Then write one sentence explaining what the technique does.

You must name the technique, not describe the smell back.

**(a) 2 marks**
Smell: **Long Method**
```javascript
function checkout(cart) {
  // 40 lines: validates items, calculates tax, applies discount, charges card, sends email
}
```
Technique name: _______________
One sentence: _______________

---

**(b) 2 marks**
Smell: **Magic Number**
```javascript
function isExpired(createdAt) {
  return Date.now() - createdAt > 2592000000;
}
```
Technique name: _______________
One sentence: _______________

---

**(c) 2 marks**
Smell: **Switch Statements (type code switching)**
```javascript
class Shape {
  area() {
    if (this.type === "circle") return Math.PI * this.r ** 2;
    if (this.type === "square") return this.side ** 2;
  }
}
```
Technique name: _______________
One sentence: _______________

---

**(d) 2 marks**
Smell: **Divergent Change**
```javascript
// The Report class is modified whenever the data format changes,
// AND whenever the output destination (PDF / CSV / screen) changes.
class Report { /* ... */ }
```
Technique name: _______________
One sentence: _______________

---

## Q2. Factory Method — Fresh Scenario (15 marks)

You are building a payment system. It supports three payment methods: `CreditCard`, `PayPal`, and `BankTransfer`. Each has a `pay(amount)` method that logs a message like:
- `[CreditCard] Charged $50`
- `[PayPal] Sent $50`
- `[BankTransfer] Transferred $50`

Client code should never call `new CreditCard()` directly — it should always go through a factory.

**Requirements:**
1. Define a base `PaymentMethod` class with a `pay(amount)` method that throws if not overridden.
2. Define three concrete classes: `CreditCard`, `PayPal`, `BankTransfer`.
3. Define `PaymentFactory` with a static `create(type)` method.
4. Write a usage example showing a client creating and using a payment method without knowing the concrete type.

**After your code:**
- Name the two participants that the client code depends on. (Hint: it is not the concrete classes.)
- In one sentence, explain how adding a fourth payment method (`Crypto`) follows the Open/Closed Principle.

---

## Q3. Observer — Fresh Scenario (12 marks)

A weather station tracks temperature. Multiple displays need to be updated when the temperature changes: a `PhoneDisplay` and a `WebDashboard`.

```javascript
class WeatherStation {
  constructor() {
    this.temperature = 0;
    // TODO
  }

  setTemperature(temp) {
    // TODO: update temperature and notify all observers
  }
}
```

**Requirements:**
1. Add `subscribe(observer)` and `unsubscribe(observer)` to `WeatherStation`.
2. `setTemperature(temp)` must update `this.temperature` and call `update(temp)` on every subscriber.
3. Implement `PhoneDisplay` with an `update(temp)` method that logs: `[Phone] Temp: 22°C`
4. Implement `WebDashboard` with an `update(temp)` method that logs: `[Web] Current temperature is 22°C`
5. Write a usage example: create the station, subscribe both displays, call `setTemperature(22)`, then `unsubscribe` one display and call `setTemperature(18)` — show the expected output.

**After your code:**
- In one sentence, explain why `WeatherStation` does not need to know what `PhoneDisplay` or `WebDashboard` do internally.

---

## Q4. Decorator — Fresh Scenario (15 marks)

You have a base `TextFormatter` class with a `format(text)` method that returns the text unchanged.

```javascript
class TextFormatter {
  format(text) {
    return text;
  }
}
```

Using the **Decorator** pattern, add two optional behaviors:
- `UpperCaseFormatter`: returns the text in uppercase
- `ExclamationFormatter`: appends `!` to the text

**Requirements:**
1. Create a base `FormatterDecorator` wrapper class that holds a reference to another formatter and delegates `format()` to it.
2. Create `UpperCaseFormatter` and `ExclamationFormatter` as concrete decorators.
3. All decorators must be stackable. Demonstrate this stacked call:
   ```javascript
   const f = new ExclamationFormatter(new UpperCaseFormatter(new TextFormatter()));
   console.log(f.format("hello"));  // expected: "HELLO!"
   ```
4. Trace the call chain for the stacked example above step by step — which `format()` runs first, second, third, and what each one returns.

**After your code:**
- In one sentence, explain why the Decorator pattern is better here than creating a `UpperCaseExclamationFormatter` subclass directly.

---

## Q5. Rate Limiter — Fresh Context (8 marks) (Bonus)

Implement a rate limiter for an API endpoint. This time the context is different: instead of tracking by `userId`, track by `ipAddress`.

```javascript
class ApiRateLimiter {
  constructor(maxCalls, windowMs) {
    // TODO
  }

  isAllowed(ipAddress) {
    // TODO: return true if allowed, false if rate limit exceeded
  }
}
```

**Requirements:**
- Use a `Map` to store timestamps per IP address.
- Prune timestamps older than `windowMs` on every call.
- Return `true` if the IP has made fewer than `maxCalls` requests in the current window, `false` otherwise.

**After your code:**
- State time and space complexity with one sentence of justification each.
- Name one bug from your original rate limiter submission yesterday and explain how this version fixes it.

---

## Gate Pass Criteria

| Requirement | Must |
|---|---|
| Q1 | Technique name is correct for all 4 — not the smell, not the category |
| Q2 | Working code with all 3 concrete classes + factory + usage example |
| Q3 | Working observer loop with subscribe, unsubscribe, and correct output trace |
| Q4 | Working stacked decorator + correct step-by-step trace |
| Q5 | Working rate limiter with Map, pruning, guard, and true/false return |
| All | No blanks |

**Pass threshold: 38 / 50 (76%) — advance to Day 21**
**Below 38: repeat the weakest question with one more drill, then gate again**
