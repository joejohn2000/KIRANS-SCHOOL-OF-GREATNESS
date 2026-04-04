# APRIL 3 ASSESSMENT | ANSWER SHEET
**Date:** April 3, 2026
**For:** Examiner / Self-check use only

---

## SECTION A: REFACTORING CATALOG & CLEAN CODE (40 marks)

---

### Q1. Identify the Code Smell (10 marks)

**Snippet A**
- Category: **OO Abuser**
- Smell: **Replace Type Code with Class** (or the symptom is a Switch Statement smell)
- Problem: The integer type codes have no semantic meaning and every new type requires editing this function; the logic is closed to extension and open to modification, which is exactly backwards.

**Snippet B**
- Category: **Coupler**
- Smell: **Message Chains** (also acceptable: Law of Demeter violation)
- Problem: The function drills through multiple levels of object navigation (`order.customer.address.country.taxRate`). Any structural change in any intermediate object breaks this line — high coupling across the entire object graph.

**Snippet C**
- Category: **Bloater**
- Smell: **Large Class** (also known as God Object)
- Problem: The class has taken on too many unrelated responsibilities. Changes to any one responsibility risk breaking the others, and the class cannot be tested or reused in isolation.

**Snippet D**
- Category: **Change Preventer**
- Smell: **Parallel Inheritance Hierarchies** or more precisely **Switch Statements** (type-code switching on shape)
- Problem: Every time a new shape is added, every conditional block across the codebase must be found and updated. The code is not closed for modification.

**Snippet E**
- Category: **Change Preventer**
- Smell: **Shotgun Surgery**
- Problem: A single change (the DB schema) requires editing 17 different call sites. There is no central abstraction; each caller knows too much about the internals.

---

### Q2. Apply the Refactoring Technique (20 marks)

**Part A — Extract Method**

Technique: **Extract Method**

```javascript
function printInvoice(order) {
  printHeader(order);
  const total = printItems(order.items);
  printFooter(total);
}

function printHeader(order) {
  console.log("=== INVOICE ===");
  console.log(`Customer: ${order.customerName}`);
  console.log(`Date: ${new Date().toISOString()}`);
}

function printItems(items) {
  let total = 0;
  for (const item of items) {
    console.log(`${item.name}: $${item.price}`);
    total += item.price;
  }
  return total;
}

function printFooter(total) {
  console.log(`Total: $${total}`);
  console.log("===============");
}
```

---

**Part B — Replace Temp with Query**

Technique: **Replace Temp with Query**

```javascript
function basePrice(product) {
  return product.quantity * product.itemPrice;
}

function getDiscountedPrice(product) {
  if (basePrice(product) > 1000) {
    return basePrice(product) * 0.9;
  }
  return basePrice(product);
}
```

Trade-off: If `basePrice` is computationally expensive (e.g., it hits a database or does a heavy calculation), extracting it to a query means it gets called multiple times. In that case, keeping the temp variable (or memoizing the result) is better. The refactoring is safest when the extracted method is purely derived from its arguments and cheap to recompute.

---

**Part C — Replace Type Code with Polymorphism**

Techniques applied:
1. **Replace Type Code with Subclasses** — create a subclass per type instead of a type field
2. **Extract Method** — each subclass implements `getBonus()` and `getTitle()` directly

```javascript
class Employee {
  constructor(name) {
    this.name = name;
  }

  getBonus() {
    throw new Error("getBonus() must be implemented by subclass");
  }

  getTitle() {
    throw new Error("getTitle() must be implemented by subclass");
  }
}

class Engineer extends Employee {
  getBonus() { return 5000; }
  getTitle() { return "Software Engineer"; }
}

class Manager extends Employee {
  getBonus() { return 10000; }
  getTitle() { return "Engineering Manager"; }
}

class Intern extends Employee {
  getBonus() { return 0; }
  getTitle() { return "Intern"; }
}

// Factory to replace the constructor type argument
function createEmployee(name, type) {
  if (type === "engineer") return new Engineer(name);
  if (type === "manager") return new Manager(name);
  if (type === "intern") return new Intern(name);
  throw new Error(`Unknown type: ${type}`);
}
```

Why the base class has no conditionals: each concrete type owns its own behavior. Adding a new employee type means adding a new subclass, not modifying existing code. This is the Open/Closed Principle applied.

---

### Q3. Technical Debt (10 marks)

**Part A**

Technical debt is the accumulated cost of taking shortcuts or making sub-optimal decisions in code that must eventually be paid back through refactoring, increased maintenance time, or rework.

- **Deliberate technical debt**: The team knowingly takes a shortcut to meet a deadline and records it as a known liability. Example: hardcoding a configuration value now and scheduling a config-service integration for next sprint.
- **Inadvertent technical debt**: The team introduces a problem without realising it — usually due to lack of knowledge or poor design instincts. Example: writing deeply nested conditionals because the developer did not know about the Replace Conditional with Polymorphism technique.

**Part B**

Two smells:
1. **Magic Number** (Dispensable) → Technique: **Replace Magic Number with Symbolic Constant**
   ```javascript
   const ONE_DAY_MS = 86400000;
   const TIMEOUT = ONE_DAY_MS;
   ```
2. **TODO Comment** (Dispensable) → Technique: the TODO itself is a Lazy Class / comment smell; the fix is either doing the work now or creating a tracked ticket and removing the inline comment.

**Part C**

Change Preventer smells make every future change more expensive, which is the core mechanism of technical debt — costs deferred to later compound over time.

- **Divergent Change**: One class must be modified in different ways for different reasons. Any time a new payment provider, new report type, or new external system is added, the same class changes again — unrelated changes collide, making each change riskier and slower.
- **Shotgun Surgery**: One logical change requires edits in many places across the codebase. The developer must find and update every affected file, and missing even one causes a bug. This makes changes slow and error-prone and discourages refactoring.

---

## SECTION B: DESIGN PATTERNS (35 marks)

---

### Q4. Pattern Classification (10 marks)

**(a) Singleton**
- Category: **Creational**
- Problem: Ensures a class has only one instance and provides a global access point to it.
- Key participants: `Singleton` class with a private constructor and a static `getInstance()` method.

**(b) Adapter**
- Category: **Structural**
- Problem: Converts the interface of a class into another interface that clients expect, allowing incompatible interfaces to work together.
- Key participants: `Target` (expected interface), `Adaptee` (existing incompatible class), `Adapter` (wraps Adaptee and implements Target).

**(c) Observer**
- Category: **Behavioral**
- Problem: Defines a one-to-many dependency so that when one object changes state, all dependents are notified automatically.
- Key participants: `Subject` (maintains subscriber list, notifies on change), `Observer` (interface with `update()` method), concrete observers.

**(d) Factory Method**
- Category: **Creational**
- Problem: Defines an interface for creating an object but lets subclasses (or a factory class) decide which class to instantiate, decoupling object creation from usage.
- Key participants: `Creator` (declares factory method), `ConcreteCreator` (overrides factory method), `Product` (created object interface), `ConcreteProduct`.

**(e) Decorator**
- Category: **Structural**
- Problem: Attaches additional responsibilities to an object dynamically, as a flexible alternative to subclassing for extending functionality.
- Key participants: `Component` (interface), `ConcreteComponent` (base implementation), `Decorator` (wraps a Component), `ConcreteDecorator` (adds behavior before/after delegation).

---

### Q5. Factory Method Implementation (12 marks)

```javascript
// Base class (the "Product" interface)
class Notifier {
  send(message) {
    throw new Error("send() must be implemented");
  }
}

// Concrete Products
class EmailNotifier extends Notifier {
  send(message) {
    console.log(`[EMAIL] ${message}`);
  }
}

class SMSNotifier extends Notifier {
  send(message) {
    console.log(`[SMS] ${message}`);
  }
}

class PushNotifier extends Notifier {
  send(message) {
    console.log(`[PUSH] ${message}`);
  }
}

// Factory (the "Creator")
class NotifierFactory {
  static create(type) {
    if (type === "email") return new EmailNotifier();
    if (type === "sms") return new SMSNotifier();
    if (type === "push") return new PushNotifier();
    throw new Error(`Unknown notifier type: ${type}`);
  }
}

// Client usage — no knowledge of concrete classes
const notifier = NotifierFactory.create("email");
notifier.send("Your order has shipped.");
```

**Open/Closed Principle**: The client code and base `Notifier` class never change when a new channel is added. A new `SlackNotifier` class can be added and registered in the factory without touching any existing code.

**Why Creational, not Structural**: This pattern is about *how objects are created* — it centralises and abstracts the instantiation logic. Structural patterns deal with *how objects are composed* after they exist (inheritance hierarchies, wrapping, bridging). The factory's job ends once the object is created.

---

### Q6. Structural vs Behavioral (13 marks)

**Part A — Decorator**

```javascript
// Base component
class Logger {
  log(message) {
    console.log(message);
  }
}

// Base decorator wrapper
class LoggerDecorator {
  constructor(logger) {
    this.logger = logger;
  }

  log(message) {
    this.logger.log(message);
  }
}

// Concrete decorators
class TimestampLogger extends LoggerDecorator {
  log(message) {
    const timestamp = new Date().toISOString();
    this.logger.log(`[${timestamp}] ${message}`);
  }
}

class PrefixLogger extends LoggerDecorator {
  constructor(logger, prefix) {
    super(logger);
    this.prefix = prefix;
  }

  log(message) {
    this.logger.log(`${this.prefix} ${message}`);
  }
}

// Stacked usage
const logger = new TimestampLogger(new PrefixLogger(new Logger(), "[ERROR]"));
logger.log("Something went wrong");
// Output: [2026-04-03T...] [ERROR] Something went wrong
```

**Part B — Observer**

```javascript
class StockTracker {
  constructor(symbol) {
    this.symbol = symbol;
    this.price = 0;
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter(o => o !== observer);
  }

  setPrice(newPrice) {
    this.price = newPrice;
    for (const observer of this.observers) {
      observer.update(this.symbol, this.price);
    }
  }
}

// Concrete observer
class Dashboard {
  update(symbol, price) {
    console.log(`Dashboard: ${symbol} is now $${price}`);
  }
}

// Usage
const tracker = new StockTracker("AAPL");
const dashboard = new Dashboard();
tracker.subscribe(dashboard);
tracker.setPrice(182.50);
// Output: Dashboard: AAPL is now $182.5
```

---

## SECTION C: SYSTEM DESIGN (25 marks)

---

### Q7. Rate Limiter (12 marks)

```javascript
class RateLimiter {
  constructor(maxRequests, windowMs) {
    this.maxRequests = maxRequests;
    this.windowMs = windowMs;
    this.timestamps = new Map(); // userId -> number[]
  }

  allow(userId) {
    const now = Date.now();
    const windowStart = now - this.windowMs;

    if (!this.timestamps.has(userId)) {
      this.timestamps.set(userId, []);
    }

    // Prune timestamps outside the window
    const userTimestamps = this.timestamps.get(userId).filter(t => t > windowStart);
    this.timestamps.set(userId, userTimestamps);

    if (userTimestamps.length < this.maxRequests) {
      userTimestamps.push(now);
      return true;
    }

    return false;
  }
}
```

**Complexity:**
- Time: O(n) per call where n is the number of timestamps stored for that user within the window. In the worst case (high-frequency user), this is O(maxRequests) — bounded by the configured limit, so effectively O(1) in practice.
- Space: O(U × maxRequests) where U is the number of distinct users currently tracked.

**Weakness at high traffic**: Storing individual timestamps per user consumes significant memory when millions of users make requests concurrently. One alternative is a **token bucket** or **fixed window counter** approach which only stores a count and a window-start timestamp per user, reducing memory to O(U).

---

### Q8. System Design Concepts (13 marks)

**(a) CAP Theorem**
The CAP theorem states that a distributed system can guarantee at most two of three properties simultaneously: Consistency (every read receives the most recent write), Availability (every request receives a response), and Partition Tolerance (the system continues operating when network partitions occur).

- **CP — HBase**: Consistent and partition-tolerant; during a partition it will refuse reads rather than return stale data. This makes sense for financial transactions where stale data is worse than no data.
- **AP — Cassandra**: Available and partition-tolerant; during a partition it returns the best available data even if it is slightly stale. This makes sense for social feeds or shopping carts where availability matters more than perfect consistency.
- **CA — PostgreSQL** (single node): Consistent and available; but it cannot tolerate network partitions because it runs as a single node. Suitable for applications that do not need distributed deployment.

**(b) Caching — Cache-Aside Pattern**
In cache-aside, the application code is responsible for reading from and writing to the cache. On a read: check the cache first; if present (hit) return it; if absent (miss) fetch from the database, store in the cache, then return. You would NOT want caching when data changes extremely frequently (cache thrash with no benefit), when data must always be strongly consistent (financial balances, inventory counts), or when the cache is shared across multiple services with complex invalidation requirements.

**(c) Scalability**
Vertical scaling means adding more resources (CPU, RAM) to an existing server. Horizontal scaling means adding more servers and distributing load across them. Choose vertical when the application is stateful and hard to distribute (e.g., a single legacy database server hitting a resource ceiling). Choose horizontal when the workload is stateless and can be load-balanced (e.g., web application servers handling HTTP requests).

**(d) SQL vs NoSQL**
SQL is better when:
1. You have relational data with complex joins and foreign-key relationships (e.g., an e-commerce system with orders, customers, and products that must stay consistent).
2. You need ACID transactions across multiple tables (e.g., a banking system where a debit and credit must both succeed or both fail).

NoSQL is better when:
1. You need to scale writes horizontally across many nodes and your data is document-shaped with no rigid schema (e.g., a CMS storing heterogeneous article metadata).
2. You need extremely low-latency key-value lookups at very high throughput (e.g., a session store or real-time leaderboard using Redis).

---

## MARKS BREAKDOWN

| Section | Question | Max | Notes |
|---|---|---:|---|
| A | Q1 Identify smells | 10 | 2 per snippet — 1 for name, 1 for explanation |
| A | Q2a Extract Method | 5 | 2 technique name, 3 code quality |
| A | Q2b Replace Temp | 5 | 2 technique name, 2 code, 1 trade-off |
| A | Q2c Type Code → Poly | 10 | 3 technique names, 5 code correctness, 2 explanation |
| A | Q3 Technical Debt | 10 | 4 + 3 + 3 per sub-part |
| B | Q4 Classification | 10 | 2 per pattern |
| B | Q5 Factory Method | 12 | 4 code, 4 OCP explanation, 4 Creational justification |
| B | Q6a Decorator | 7 | 4 code, 3 stacking example |
| B | Q6b Observer | 6 | 4 code, 2 concrete observer |
| C | Q7 Rate Limiter | 12 | 6 code, 3 complexity, 3 weakness |
| C | Q8 System Design | 13 | per sub-part as marked |
| **Total** | | **100** | |
