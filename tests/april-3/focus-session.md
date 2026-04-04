# APRIL 3 FOCUS SESSION | Refactoring Techniques + Pattern Implementation
**Date:** April 3, 2026
**Trigger:** 37/100 on April 3 paper; Q5 and Q6 entirely blank; smell/technique confusion throughout; rate limiter broken in 5 places

---

## What Passed — Skip These

- Smell identification from code (Q1): mostly reliable — no drill needed here
- System design concepts (Q8b scalability, Q8d SQL/NoSQL): solid — no drill needed
- Subclass inheritance shape: the structure of `extends` and method override is understood

---

## What Failed and Why It Matters

### Gap 1: You are naming smells when asked for techniques

Every Q2 answer did this:
- Q2a: named "Long Method" (smell) instead of "Extract Method" (technique)
- Q2b: named "Inline Class" (completely wrong) instead of "Replace Temp with Query"
- Q2c: named "Switch Statements" (smell) instead of "Replace Type Code with Subclasses"

**Why it matters:** In a code review or interview, "I saw a Long Method smell so I used Long Method" is meaningless. The technique name is the action. The smell is the diagnosis. You need both and they are different words.

**The rule:** Smell = what is wrong. Technique = what you do about it.

| Smell | Technique |
|---|---|
| Long Method | Extract Method |
| Temp variable that could be a query | Replace Temp with Query |
| Type code with if/switch on type | Replace Type Code with Subclasses |
| Message Chain | Hide Delegate |
| Magic Number | Replace Magic Number with Symbolic Constant |
| Shotgun Surgery | Move Method / Move Field (consolidate) |
| Divergent Change | Extract Class |

**Drill — do this now, no looking up:**
For each smell, write the technique name from memory. Then flip it: given a technique name, write the smell it fixes.

---

### Gap 2: Pattern implementation — you know what they do but can't write them

Q5 (Factory Method) and Q6 (Decorator + Observer) were left entirely blank. This is the same gap that has appeared in every fresh paper: concept recognition is ahead of blank-page execution.

**The three patterns you must be able to write from scratch:**

---

#### Pattern Drill A — Factory Method

The shape is always:
1. A base class / interface with the method signature
2. Concrete classes that implement it
3. A factory with a `create(type)` static method

Write this from memory right now:

```javascript
// Step 1: base class
class Notifier {
  send(message) { throw new Error("not implemented"); }
}

// Step 2: concrete classes
class EmailNotifier extends Notifier { /* ... */ }
class SMSNotifier extends Notifier { /* ... */ }

// Step 3: factory
class NotifierFactory {
  static create(type) {
    if (type === "email") return new EmailNotifier();
    if (type === "sms") return new SMSNotifier();
    throw new Error("unknown type");
  }
}

// Step 4: client — never uses new EmailNotifier() directly
const n = NotifierFactory.create("email");
n.send("hello");
```

**Your drill:** Close this file and write the above from scratch. Then add a third notifier type (`PushNotifier`) without touching the existing notifier classes. That is the Open/Closed Principle in action — you added a new concrete class and registered it in the factory; nothing else changed.

---

#### Pattern Drill B — Observer

The shape is always:
1. Subject: has `subscribe`, `unsubscribe`, and a `notify` loop
2. Observers: each has an `update()` method
3. Subject calls `update()` on all observers when state changes

Write this from memory right now:

```javascript
class StockTracker {
  constructor(symbol) {
    this.symbol = symbol;
    this.price = 0;
    this.observers = [];           // always an array, always starts empty
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter(o => o !== observer);
  }

  setPrice(newPrice) {
    this.price = newPrice;
    for (const obs of this.observers) {
      obs.update(this.symbol, this.price);   // notify all
    }
  }
}

class Dashboard {
  update(symbol, price) {
    console.log(`[Dashboard] ${symbol}: $${price}`);
  }
}
```

**Your drill:** Write it from scratch. Then add an `AlertService` observer that prints a warning if the price goes above 200. The `StockTracker` class must not change at all — you only add the new observer.

---

#### Pattern Drill C — Decorator

The shape is always:
1. A base component class with the core method
2. A decorator wrapper that holds a reference to a component and delegates to it
3. Concrete decorators extend the wrapper and add behavior before or after the delegation

Write this from memory right now:

```javascript
// 1. Base
class Logger {
  log(message) { console.log(message); }
}

// 2. Base decorator (the wrapper template)
class LoggerDecorator {
  constructor(logger) { this.logger = logger; }
  log(message) { this.logger.log(message); }  // pure delegation by default
}

// 3. Concrete decorators
class TimestampLogger extends LoggerDecorator {
  log(message) {
    this.logger.log(`[${new Date().toISOString()}] ${message}`);
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

// Stacking — read from inside out: Logger → PrefixLogger → TimestampLogger
const logger = new TimestampLogger(new PrefixLogger(new Logger(), "[ERROR]"));
logger.log("disk full");
// Output: [2026-04-03T...] [ERROR] disk full
```

**Key rule to memorise:** The decorator wraps something that has the same interface. The stacking order means the outermost decorator runs first.

**Your drill:** Write it from scratch. Then add a `UpperCaseLogger` that logs all messages in uppercase. Stack it between `PrefixLogger` and `TimestampLogger` and trace the output.

---

### Gap 3: Rate Limiter — five specific bugs to understand and fix

The concept was right. The code had five bugs. Understand each one:

**Bug 1 — Property name mismatch**
```javascript
// Constructor declared:
this.user = [];
// allow() tried to use:
this.users[userId]   // this.users does not exist
```
Fix: use `this.users = new Map()` in the constructor, then `this.users.get(userId)` in `allow`.

**Bug 2 — Wrong data structure**
An array cannot store per-userId data. You need a `Map` because you need to look up timestamps by userId (a string key).

**Bug 3 — No pruning**
The rate limiter must remove timestamps older than the window on every call. Without this step, old requests keep counting toward the limit forever and no user ever gets unblocked.
```javascript
const userTimestamps = this.users.get(userId).filter(t => t > windowStart);
```

**Bug 4 — No guard check**
After pruning, the function never checks whether the remaining count is below `maxRequests`. That check is the entire point of the rate limiter.
```javascript
if (userTimestamps.length < this.maxRequests) {
  userTimestamps.push(now);
  return true;
}
return false;
```

**Bug 5 — `allow()` returns nothing**
The function signature says `allow(userId)` must return `true` or `false`. The candidate's code had `Return user;` outside the method body with an uppercase R — a syntax error, not a valid return statement.

**Your drill:** Write the complete working `RateLimiter` from scratch with all five fixes. Trace it manually: create a limiter with `maxRequests=2, windowMs=5000`. Call `allow("u1")` three times. The first two should return `true`, the third `false`. Then wait (conceptually) 6 seconds and call again — it should return `true`.

---

## Verification Gate — do this after the drills

Answer all four from memory, no notes:

1. What is the difference between a smell and a technique? Give one example of each from the refactoring catalog.
2. Write `NotifierFactory` with three concrete notifier types. Do not look at your notes.
3. Write `StockTracker` with `subscribe`, `unsubscribe`, `setPrice`, and one concrete observer. Do not look at your notes.
4. Write a working `RateLimiter` with pruning, the maxRequests guard, and a correct `true`/`false` return.

**Gate pass criteria:**
- All four answered from scratch
- Code runs without syntax errors
- Technique names and smell names are not confused in the explanation
- No blanks

---

## What Comes Next

After this focus session and the four-question verification gate: short gate test to confirm readiness, then advance to Day 21 (HTML5 and Accessibility).

Do not advance without the gate. The evidence from this repo is clear: narrow recovery works, but must be verified on a fresh prompt before it counts as stable.
