# ANSWER KEY | JAVASCRIPT DEEP DIVE - MARCH 14

---

## WARM-UP: Quick Fire

```javascript
a) console.log(typeof NaN);
   Answer: "number" (NaN is technically a number!)

b) console.log(0.1 + 0.2 === 0.3);
   Answer: false (floating point precision issue - 0.1 + 0.2 = 0.30000000000000004)

c) [] + [];
   Answer: "" (empty string - array's toString() returns "", then concatenation)

d) [] + {};
   Answer: "[object Object]" (array.toString() = "", {}.toString() = "[object Object]")

e) {} + [];
   Answer: 0 ({} is parsed as empty block, +[] is unary plus, coerces [] to 0)
```

---

## SECTION A: The Execution Context & Scope Chain

### Q1. Tracing the Scope Chain

**1. Output:**
```
Running module: Module-4
Running module: Module-4
Running module: Module-4
```
(Because i becomes 4 after the loop ends)

**2. Why this happens:**
- `var i` is function-scoped, not block-scoped
- There's only ONE `i` variable in the entire function scope
- By the time any `handler()` executes, the loop has finished and `i = 4`
- Each closure captures the SAME `i` variable reference
- The `name` parameter is also captured by reference in each handler

**3. Fix using let:**
```javascript
for (let i = 1; i <= 3; i++) {
  registerModule("Module-" + i);
}
// OR using IIFE
for (var i = 1; i <= 3; i++) {
  (function(captured) {
    registerModule("Module-" + captured);
  })(i);
}
```

### Q2. The Shadowing Puzzle

**Output:** `middle`

**Explanation:**
- JavaScript uses lexical scoping - scope is determined by WHERE FUNCTIONS ARE WRITTEN, not where they're called
- When `inner()` runs, it looks for `x`:
  1. First checks inner's own scope - not found
  2. Then checks middle's scope - FOUND `x = "middle"`
  3. Never looks at outer's or global's `x` because it already found it
- This is called "shadowing" - the inner `x` shadows the outer `x`

**Scope chain:** inner → middle → outer → global

### Q3. Hoisting Edge Case

**Output:** 
```
undefined
undefined
```

**Explanation:**
- `var` declarations are hoisted to the top of their function scope
- The ENTIRE declaration (but NOT the assignment) is hoisted
- So the code effectively becomes:
```javascript
function test() {
  var value; // hoisted, initialized as undefined
  console.log(value); // undefined
  
  if (false) {
    value = "I am never executed"; // never runs, but declaration exists
  }
  
  console.log(value); // undefined
}
test();
```
- Even though the if block never executes, the variable declaration is still hoisted

---

## SECTION B: Closures in the Wild

### Q4. The Module Pattern

**Implementation:**
```javascript
function createPreferencesManager() {
  // Private internal store
  var _internalStore = {};
  
  // Private defaults
  var _defaults = {
    theme: 'light',
    language: 'en',
    notifications: true
  };
  
  // Initialize with defaults
  Object.keys(_defaults).forEach(key => {
    _internalStore[key] = _defaults[key];
  });
  
  // Return public API
  return {
    get: function(key) {
      return _internalStore[key];
    },
    set: function(key, value) {
      _internalStore[key] = value;
    },
    reset: function() {
      _internalStore = {};
      Object.keys(_defaults).forEach(key => {
        _internalStore[key] = _defaults[key];
      });
    }
  };
}
```

**Why internal store is not accessible:**
- `_internalStore` is a variable in the function's local scope
- Only the returned object methods can access it (closure)
- External code has no reference to `_internalStore` - it's completely private
- Unlike class private fields (#), there's no enforcement - it's by convention

### Q5. The Classic Closure-in-Loop Bug

**1. What actually prints:**
```
4
4
4
```
(Because i = 4 after loop ends, all three functions share the same i)

**2. Three fixes:**

**Approach 1: Using let (ES6)**
```javascript
for (let i = 1; i <= 3; i++) {
  functions.push(function() {
    console.log(i);
  });
}
```
- `let` creates a new binding for each iteration

**Approach 2: Using IIFE**
```javascript
for (var i = 1; i <= 3; i++) {
  (function(captured) {
    functions.push(function() {
      console.log(captured);
    });
  })(i);
}
```
- IIFE creates a new scope, capturing the current value

**Approach 3: Using factory function**
```javascript
function createLogger(n) {
  return function() {
    console.log(n);
  };
}

for (var i = 1; i <= 3; i++) {
  functions.push(createLogger(i));
}
```
- Factory function creates a new scope for each call

### Q6. The Currying Challenge

**Part A - curry implementation:**
```javascript
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    }
    return function(...nextArgs) {
      return curried.apply(this, args.concat(nextArgs));
    };
  };
}
```

**Part B - multiplyBy implementation:**
```javascript
function multiplyBy(n) {
  return function(x) {
    return n * x;
  };
}
```

**How closures make this possible:**
- Each returned function captures the outer function's parameters in its closure
- For currying: each successive call captures the accumulated arguments
- For multiplyBy: the returned function "remembers" the value of n

---

## SECTION C: The Execution Order Puzzle

### Q7. Event Loop & Microtasks

**Exact Output Order:**
```
1: Start
7: End
3: Promise 1
4: Promise 2
2: Timeout
5: Timeout 2
6: Promise in Timeout
```

**Explanation:**

1. `console.log('1: Start')` - runs immediately
2. `setTimeout` - added to macrotask queue (will run later)
3. `Promise.resolve().then()` - added to microtask queue
4. Another `setTimeout` - added to macrotask queue
5. `console.log('7: End')` - runs immediately
6. Call stack is empty → check microtask queue FIRST
   - Promise 1 runs, prints
   - Promise 2 runs, prints
7. Microtask queue empty → check macrotask queue
   - First timeout runs, prints "2"
   - Inside timeout, another Promise is queued to microtask
8. Check microtask queue again
   - Promise in timeout runs, prints "6"
9. Macrotask queue empty, done

**Key points:**
- Microtasks ALWAYS run before macrotasks
- Promises go to microtask queue (then/catch/finally)
- setTimeout goes to macrotask queue
- After each macrotask, all microtasks are drained before next macrotask

### Q8. Private Data with Closures

**Implementation:**
```javascript
function createCounter() {
  var count = 0;  // Private variable
  
  return {
    increment: function() {
      count++;
      return count;
    },
    decrement: function() {
      count--;
      return count;
    },
    getValue: function() {
      return count;
    },
    reset: function() {
      count = 0;
      return count;
    }
  };
}
```

**Output:**
```
1  // increment
2  // increment  
2  // getValue
1  // decrement
0  // reset
0  // getValue
```

**Direct access attempt:**
```javascript
console.log(counter.count); // undefined
```
- Returns undefined because count is not a property of the returned object

**Why closures provide privacy:**
- The `count` variable exists only in the function's scope
- No way to access it except through the returned methods
- Unlike class private fields (#), this is "enforced" by JavaScript's scoping, not the language
- It's truly private - there's no reference to count outside the function

---

## BONUS: Q9. Execution Context Deep Dive

**Answer:**
```
10
```

**Explanation:**
1. **What logs:** 10

2. **Why not 20:** JavaScript uses LEXICAL scoping (also called static scoping)
   - The scope of a function is determined WHERE IT IS DEFINED, not where it is called
   - `foo` is defined in global scope, so it looks for x in global scope
   - When `fn()` is called inside `bar`, it still looks for x in its lexical environment (global), not bar's scope

3. **Dynamic scoping alternative:** If JS used dynamic scoping, it would print 20
   - Dynamic scoping determines scope at CALL TIME, not definition time
   - Few languages use this (Emacs Lisp, some shell languages)

4. **Why lexical is better for JavaScript:**
   - Predictable - you can determine what a variable refers to by reading the code
   - Enables closures to work reliably
   - Makes code more readable and debuggable
   - Allows for function decorators, higher-order functions, etc.

---

## SCORING

Calculate your total:

| Section | Max | Your Score |
|---------|-----|------------|
| Warm-up | 10 | ___ |
| Section A | 25 | ___ |
| Section B | 35 | ___ |
| Section C | 30 | ___ |
| Bonus | +10 | ___ |
| **TOTAL** | **100** | ___ |

| Score | Level | Action |
|-------|-------|--------|
| 90-100 | Ninja | Ready for advanced topics |
| 80-89 | Strong | Minor refinements needed |
| 70-79 | Building | More practice on closures |
| 60-69 | Learning | Review fundamentals again |
| Below 60 | Foundation | Repeat core JS concepts |