# APRIL 3 ASSESSMENT | DAY 20 + REFACTORING & DESIGN PATTERNS
**Date:** April 3, 2026
**Focus:** System design vocabulary (Day 20), Refactoring catalog & techniques, Clean code, Technical debt, and Design pattern classification
**Total Marks:** 100
**Time Allowed:** 120 minutes

---

> "Name the smell. Name the technique. Fix the code. Then explain why."

---

## Instructions

1. Answer in JavaScript unless a question explicitly says otherwise.
2. No blanks allowed. If you are unsure, write your best attempt and explain your reasoning.
3. For refactoring questions: name the smell first, then name the technique, then write the refactored code.
4. For design-pattern questions: name the category, then explain the role of each participant.
5. Before submitting any code, mentally run one normal case and one edge case.
6. Complexity justification is required wherever code is written.

---

## SECTION A: REFACTORING CATALOG & CLEAN CODE (40 marks)

### Q1. Identify the Code Smell (10 marks)

Each snippet below contains exactly one named code smell from the catalog. For each one:
- Name the smell (use the catalog category: Bloater / OO Abuser / Change Preventer / Dispensable / Coupler)
- Name the specific smell within that category
- Write one sentence explaining what makes it a problem

**Snippet A (2 marks)**
```javascript
function getPrice(type) {
  if (type === 1) return 100;
  if (type === 2) return 200;
  if (type === 3) return 150;
  if (type === 4) return 300;
}
```

**Snippet B (2 marks)**
```javascript
function processOrder(order) {
  const tax = order.customer.address.country.taxRate * order.total;
  const discount = order.customer.membershipLevel.discountPercent * order.total;
  return order.total + tax - discount;
}
```

**Snippet C (2 marks)**
```javascript
// This class has 800 lines of code, 40 methods, and handles:
// - user authentication
// - email sending
// - PDF generation
// - payment processing
// - logging
class AppManager { /* ... */ }
```

**Snippet D (2 marks)**
```javascript
function calculateArea(shape) {
  if (shape.type === "circle") return Math.PI * shape.radius ** 2;
  if (shape.type === "rectangle") return shape.width * shape.height;
  if (shape.type === "triangle") return 0.5 * shape.base * shape.height;
}
```

**Snippet E (2 marks)**
```javascript
function getUserData(id) {
  const result = db.query(`SELECT * FROM users WHERE id = ${id}`);
  return result;
}
// Note: This function is called in 17 different files. The DB schema is changing next week.
```

---

### Q2. Apply the Refactoring Technique (20 marks)

For each problem below, name the technique(s) from the catalog, then write the refactored code.

**Part A — Extract Method (5 marks)**

Refactor this function. It does too much in one place.

```javascript
function printInvoice(order) {
  // Print header
  console.log("=== INVOICE ===");
  console.log(`Customer: ${order.customerName}`);
  console.log(`Date: ${new Date().toISOString()}`);

  // Print items
  let total = 0;
  for (const item of order.items) {
    console.log(`${item.name}: $${item.price}`);
    total += item.price;
  }

  // Print footer
  console.log(`Total: $${total}`);
  console.log("===============");
}
```

Name the technique. Write the refactored version.

---

**Part B — Replace Temp with Query (5 marks)**

```javascript
function getDiscountedPrice(product) {
  const basePrice = product.quantity * product.itemPrice;
  if (basePrice > 1000) {
    return basePrice * 0.9;
  }
  return basePrice;
}
```

Name the technique. Rewrite it so `basePrice` is no longer a temp variable.

After your code: explain one trade-off of this refactoring (when might keeping the temp be better?).

---

**Part C — Replace Type Code with Polymorphism (10 marks)**

This code uses a type code to switch behavior. Refactor it using a subclass approach.

```javascript
class Employee {
  constructor(name, type) {
    this.name = name;
    this.type = type; // "engineer", "manager", "intern"
  }

  getBonus() {
    if (this.type === "engineer") return 5000;
    if (this.type === "manager") return 10000;
    if (this.type === "intern") return 0;
  }

  getTitle() {
    if (this.type === "engineer") return "Software Engineer";
    if (this.type === "manager") return "Engineering Manager";
    if (this.type === "intern") return "Intern";
  }
}
```

Requirements:
- Use subclasses for each employee type
- The base class should not contain any `if/switch` on type
- Name every technique you applied

---

### Q3. Technical Debt Question (10 marks)

**Part A (4 marks):**
Define technical debt. Explain the difference between **deliberate** technical debt and **inadvertent** technical debt. Give a concrete example of each.

**Part B (3 marks):**
A team has this in their codebase:

```javascript
// TODO: fix this properly later — using magic number for now
const TIMEOUT = 86400000;
```

Name two code smells present here. For each, name the exact refactoring technique that would fix it.

**Part C (3 marks):**
What is the relationship between the **Change Preventer** category of smells and technical debt? Name two specific Change Preventer smells and explain how each one makes future changes harder.

---

## SECTION B: DESIGN PATTERNS (35 marks)

### Q4. Pattern Classification (10 marks)

For each pattern below, state:
1. The category (Creational / Structural / Behavioral)
2. The problem it solves in one sentence
3. The key participants (roles)

**(a) Singleton (2 marks)**

**(b) Adapter (2 marks)**

**(c) Observer (2 marks)**

**(d) Factory Method (2 marks)**

**(e) Decorator (2 marks)**

---

### Q5. Implement a Creational Pattern (12 marks)

Implement the **Factory Method** pattern for the following scenario:

> A notification system can send messages via Email, SMS, or Push notification. Each channel has a different implementation. The client code should not depend on concrete classes — it should only depend on the `Notifier` interface (method: `send(message)`).

Requirements:
- Define a base `Notifier` class with a `send(message)` method
- Define concrete classes: `EmailNotifier`, `SMSNotifier`, `PushNotifier`
- Define a `NotifierFactory` with a static `create(type)` method that returns the correct notifier
- Write a short usage example showing how a client would use it without knowing the concrete type

After your code:
- Explain how this satisfies the Open/Closed Principle
- State why this is classified as a Creational pattern, not Structural

---

### Q6. Structural vs Behavioral Trade-off (13 marks)

**Part A — Decorator Pattern (7 marks)**

You have a `Logger` class with a `log(message)` method. Using the **Decorator** pattern, add two optional behaviors:
- `TimestampLogger`: prefixes the message with a timestamp
- `PrefixLogger`: prefixes the message with a custom label like `[ERROR]`

Requirements:
- The base `Logger` class must remain unchanged
- Both decorators must be stackable: `new TimestampLogger(new PrefixLogger(new Logger()))`
- Write a working example showing the stacked output

**Part B — Observer Pattern (6 marks)**

A stock price tracker needs to notify multiple subscribers (Dashboard, AlertService, Logger) whenever the price changes.

```javascript
class StockTracker {
  constructor(symbol) {
    this.symbol = symbol;
    this.price = 0;
    // TODO
  }

  setPrice(newPrice) {
    // TODO: update price and notify all subscribers
  }
}
```

Implement the Observer pattern to complete this. Requirements:
- `subscribe(observer)` and `unsubscribe(observer)` methods on `StockTracker`
- Each observer has a `update(symbol, price)` method
- Write one concrete observer as an example

---

## SECTION C: DAY 20 CARRY-OVER — SYSTEM DESIGN (25 marks)

### Q7. Rate Limiter Implementation (12 marks)

Implement a sliding window rate limiter:

```javascript
class RateLimiter {
  constructor(maxRequests, windowMs) {
    // TODO
  }

  allow(userId) {
    // TODO: return true if the request is within the rate limit, false otherwise
  }
}
```

Rules:
- `maxRequests` is the maximum number of requests allowed per user per window
- `windowMs` is the window duration in milliseconds
- Prune timestamps older than the window on every `allow` call

After your code:
1. State time and space complexity with justification
2. Name one weakness of this approach at very high traffic and one way to address it

---

### Q8. System Design Concepts (13 marks)

Answer each of the following. 2–4 sentences each.

**(a) CAP Theorem (4 marks)**
Explain the CAP theorem. Give one real database for each pair: CP, AP, and CA. For each, state what it sacrifices and why that trade-off makes sense.

**(b) Caching (3 marks)**
Explain the cache-aside pattern. What happens on a cache miss? When would you NOT want to use caching?

**(c) Scalability (3 marks)**
What is the difference between vertical scaling and horizontal scaling? Give one scenario where each is the right choice.

**(d) SQL vs NoSQL (3 marks)**
Name two situations where SQL is clearly the better choice and two where NoSQL is clearly better. For each, justify your answer in one sentence.

---

## SCORING GUIDE

| Score | Interpretation |
|---|---|
| 85-100 | Strong transfer across all three domains — ready to advance |
| 70-84 | Solid overall with targeted carry-over needed |
| 55-69 | Partial transfer; one domain needs remediation before widening |
| Below 55 | Not ready for Phase 4; consolidation required |

---

*This paper tests both curriculum advancement (Day 20) and the deviation topics the candidate studied beyond the plan. All three sections carry equal weight in determining readiness to advance.*
