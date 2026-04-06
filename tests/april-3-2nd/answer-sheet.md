# APRIL 3 FOCUS GATE — ANSWER SHEET
**Date:** April 3, 2026
**For:** Examiner / Self-check use only

---

## Q1. Smell → Technique (8 marks)

**(a) Long Method → Extract Method**
Technique: **Extract Method**
What it does: Pull a coherent block of code out of a large method into its own named method, reducing the original method's length and giving each sub-task a clear name.

**(b) Magic Number → Replace Magic Number with Symbolic Constant**
Technique: **Replace Magic Number with Symbolic Constant**
What it does: Replace the raw literal with a named constant so the value's meaning is clear and can be changed from one place.

```javascript
const THIRTY_DAYS_MS = 2592000000;
function isExpired(createdAt) {
  return Date.now() - createdAt > THIRTY_DAYS_MS;
}
```

**(c) Switch Statements (type code) → Replace Type Code with Subclasses**
Technique: **Replace Type Code with Subclasses**
What it does: Replace the type field and conditional branches with a class hierarchy where each subclass provides its own implementation of the varying behaviour.

**(d) Divergent Change → Extract Class**
Technique: **Extract Class**
What it does: Split the class into two separate classes, each with a single, coherent reason to change — one responsible for data formatting, one for output destination.

---

## Q2. Factory Method — Payment System (15 marks)

```javascript
// 1. Base class (Product interface)
class PaymentMethod {
  pay(amount) {
    throw new Error("pay() must be implemented by a subclass");
  }
}

// 2. Concrete Products
class CreditCard extends PaymentMethod {
  pay(amount) {
    console.log(`[CreditCard] Charged $${amount}`);
  }
}

class PayPal extends PaymentMethod {
  pay(amount) {
    console.log(`[PayPal] Sent $${amount}`);
  }
}

class BankTransfer extends PaymentMethod {
  pay(amount) {
    console.log(`[BankTransfer] Transferred $${amount}`);
  }
}

// 3. Factory (Creator)
class PaymentFactory {
  static create(type) {
    if (type === "credit") return new CreditCard();
    if (type === "paypal") return new PayPal();
    if (type === "bank")   return new BankTransfer();
    throw new Error(`Unknown payment type: ${type}`);
  }
}

// 4. Client usage — depends only on PaymentMethod and PaymentFactory
const method = PaymentFactory.create("paypal");
method.pay(50);
// Output: [PayPal] Sent $50
```

**Two participants the client depends on:**
`PaymentMethod` (the base class / interface) and `PaymentFactory` (the creator). The client never references `CreditCard`, `PayPal`, or `BankTransfer` directly.

**Open/Closed Principle — adding Crypto:**
Add a new `Crypto` class that extends `PaymentMethod` and add one line to `PaymentFactory.create()` — no existing class is modified, only extended.

---

## Q3. Observer — Weather Station (12 marks)

```javascript
class WeatherStation {
  constructor() {
    this.temperature = 0;
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter(o => o !== observer);
  }

  setTemperature(temp) {
    this.temperature = temp;
    for (const obs of this.observers) {
      obs.update(temp);
    }
  }
}

// Concrete observers
class PhoneDisplay {
  update(temp) {
    console.log(`[Phone] Temp: ${temp}°C`);
  }
}

class WebDashboard {
  update(temp) {
    console.log(`[Web] Current temperature is ${temp}°C`);
  }
}

// Usage example
const station = new WeatherStation();
const phone = new PhoneDisplay();
const web = new WebDashboard();

station.subscribe(phone);
station.subscribe(web);
station.setTemperature(22);
// [Phone] Temp: 22°C
// [Web] Current temperature is 22°C

station.unsubscribe(web);
station.setTemperature(18);
// [Phone] Temp: 18°C
```

**Why WeatherStation does not need to know internals of its observers:**
`WeatherStation` only calls `obs.update(temp)` — it depends on the interface contract (the `update` method), not on what `PhoneDisplay` or `WebDashboard` do with the value, so either can be changed or replaced without touching `WeatherStation`.

---

## Q4. Decorator — Text Formatter (15 marks)

```javascript
// 1. Base component
class TextFormatter {
  format(text) {
    return text;
  }
}

// 2. Base decorator wrapper
class FormatterDecorator {
  constructor(formatter) {
    this.formatter = formatter;
  }

  format(text) {
    return this.formatter.format(text); // pure delegation
  }
}

// 3. Concrete decorators
class UpperCaseFormatter extends FormatterDecorator {
  format(text) {
    return this.formatter.format(text).toUpperCase();
  }
}

class ExclamationFormatter extends FormatterDecorator {
  format(text) {
    return this.formatter.format(text) + "!";
  }
}

// Stacked usage
const f = new ExclamationFormatter(new UpperCaseFormatter(new TextFormatter()));
console.log(f.format("hello")); // "HELLO!"
```

**Step-by-step call trace for `f.format("hello")`:**

1. `ExclamationFormatter.format("hello")` is called first (outermost layer).
2. It delegates to `this.formatter.format("hello")`, which calls `UpperCaseFormatter.format("hello")`.
3. `UpperCaseFormatter` delegates to `this.formatter.format("hello")`, which calls `TextFormatter.format("hello")`.
4. `TextFormatter.format("hello")` returns `"hello"` (innermost, no modification).
5. `UpperCaseFormatter` receives `"hello"`, applies `.toUpperCase()`, returns `"HELLO"`.
6. `ExclamationFormatter` receives `"HELLO"`, appends `"!"`, returns `"HELLO!"`.

**Why Decorator is better than `UpperCaseExclamationFormatter`:**
With subclassing, every combination of behaviours needs its own class (`UpperCasePlusExclamation`, `ExclamationOnly`, `UpperCaseOnly`, etc.), causing a class explosion; Decorator composes any combination at runtime with only one class per behaviour.

---

## Q5. Rate Limiter — By IP Address (8 marks)

```javascript
class ApiRateLimiter {
  constructor(maxCalls, windowMs) {
    this.maxCalls = maxCalls;
    this.windowMs = windowMs;
    this.timestamps = new Map(); // ipAddress -> number[]
  }

  isAllowed(ipAddress) {
    const now = Date.now();
    const windowStart = now - this.windowMs;

    // Initialise entry if first request from this IP
    if (!this.timestamps.has(ipAddress)) {
      this.timestamps.set(ipAddress, []);
    }

    // Prune timestamps outside the current window
    const recent = this.timestamps.get(ipAddress).filter(t => t > windowStart);
    this.timestamps.set(ipAddress, recent);

    if (recent.length < this.maxCalls) {
      recent.push(now);
      return true;
    }

    return false;
  }
}
```

**Complexity:**
- Time: O(k) per call, where k is the number of stored timestamps for that IP within the window — bounded by `maxCalls` in practice, effectively O(1).
- Space: O(N × maxCalls) where N is the number of distinct IP addresses currently tracked — one timestamp array per IP, each capped at `maxCalls` entries after pruning.

**Bug named and fixed:**
Yesterday's submission used `this.user = []` (an array) in the constructor but tried to access `this.users[userId]` in `allow()` — a property name mismatch that would throw `Cannot read properties of undefined` immediately. This version uses `this.timestamps = new Map()` consistently and accesses it with `.has()`, `.get()`, and `.set()`, so the property name is the same everywhere.

---

## Marks Breakdown

| Question | Max | Notes |
|---|---|---:|
| Q1a Extract Method | 2 | 1 technique name, 1 sentence |
| Q1b Replace Magic Number | 2 | 1 technique name, 1 sentence |
| Q1c Replace Type Code with Subclasses | 2 | 1 technique name, 1 sentence |
| Q1d Extract Class | 2 | 1 technique name, 1 sentence |
| Q2 Factory Method | 15 | 8 code, 4 participants explanation, 3 OCP sentence |
| Q3 Observer | 12 | 8 code + output trace, 4 explanation |
| Q4 Decorator | 15 | 8 code, 5 call trace, 2 explanation |
| Q5 Rate Limiter | 8 | 4 code, 2 complexity, 2 bug identified |
| **Total** | **58** | marked out of 50; Q5 is labelled Bonus — cap at 50 |
