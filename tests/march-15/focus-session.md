# Day 3 (March 15) - FOCUS SESSION
## Remediation: JavaScript Fundamentals

Based on assessment results, skip what you know. Focus ONLY on these weak areas:

---

## WHAT YOU PASSED (Skip)
- ✅ Scope chain basics (Q1, Q2)
- ✅ var vs let basics
- ✅ LEGB rule understanding
- ✅ Identifying closure problems (can spot them, just can't fix)

---

## WHAT YOU FAILED (Focus Today)

### 1. HOISTING (Critical Gap)
**Status:** 0/7 - Complete misunderstanding

**Learn This:**
- `var` declarations are hoisted to top of function
- Initialized to `undefined` (NOT uninitialized)
- Only DECLARATION hoisted, not assignment
- `let` and `const` are hoisted but NOT initialized (Temporal Dead Zone)

**Practice:**
```javascript
// Q3 WAS:
// console.log(value);  // ?
// if (false) { var value = "hi"; }
// console.log(value);  // ?

// Answer: undefined, undefined
// Because var value is hoisted as: var value; (undefined)
```

**Exercises:**
1. Predict outputs:
```javascript
console.log(a);
var a = 1;

console.log(b);
let b = 2;
```
2. Explain why the if(false) code still creates a variable

---

### 2. EVENT LOOP & MICROTASKS (Critical Gap)
**Status:** 0/15 - Completely wrong

**Learn This:**
- Microtask queue runs BEFORE macrotask queue
- Promises go to microtask (then, catch, finally)
- setTimeout goes to macrotask
- After EACH macrotask, ALL microtasks run first

**Order =**
1. Sync code runs first
2. All microtasks (promises)
3. ONE macrotask (setTimeout)
4. All microtasks again
5. Next macrotask...

**Practice:**
```javascript
// What prints first?
console.log('1');
setTimeout(() => console.log('2'), 0);
Promise.resolve().then(() => console.log('3'));
console.log('4');

// Answer: 1, 4, 3, 2
```

**Exercises:**
- Draw the event loop diagram
- Explain why Promise resolves before setTimeout

---

### 3. CLOSURES - PRACTICAL IMPLEMENTATION
**Status:** Failed Q4, Q6, Q8

**You Can:**
- Spot closure problems (Q1, Q2, Q5 output)
- Use `let` to fix (Q5 fix 1)

**You CANNOT:**
- Write module pattern (Q4)
- Write curry function (Q6)
- Write proper private counter (Q8)

**Practice Each Pattern:**

#### A. Module Pattern
```javascript
function createManager() {
  var _data = {};  // private
  
  return {
    get: function(key) { return _data[key]; },
    set: function(key, val) { _data[key] = val; }
  };
}
```
**Task:** Add a `reset()` method that clears all data

#### B. Currying
```javascript
function curry(fn) {
  return function(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    }
    return function(...more) {
      return curried.apply(this, args.concat(more));
    };
  };
}
```
**Task:** Write this out 5 times until you can do it from memory

#### C. Private Variables
```javascript
function createCounter() {
  var count = 0;  // truly private
  
  return {
    inc: function() { return ++count; },
    dec: function() { return --count; },
    get: function() { return count; }
  };
}
```
**Task:** Add `reset()` that sets count to 0

---

### 4. TYPE COERCION (Warm-up Gaps)
**Status:** Partial failure

**Learn:**
```javascript
0.1 + 0.2 === 0.3  // false! (floating point)

[] + [] = ""        // empty string
[] + {} = "[object Object]"
{} + [] = 0          // {} is block, +[] = 0
```

**Practice:** Memorize these edge cases

---

## TODAY'S PRACTICE TASKS

### Hour 1: Hoisting
1. Re-read: https://developer.mozilla.org/en-US/docs/Glossary/Hoisting
2. Write 10 hoisting predictions, verify in console
3. Explain to yourself why Q3 was wrong

### Hour 2: Event Loop  
1. Watch: https://www.youtube.com/watch?v=8aGhZQkoFbQ (Philip Roberts)
2. Draw the event loop from memory
3. Re-predict Q7, verify in Node.js

### Hour 3: Closure Patterns
1. Write module pattern 5x from memory
2. Write curry function 5x from memory
3. Write private counter 5x from memory

### Hour 4: Type Coercion
1. Memorize the edge cases
2. Quiz yourself

### Hour 5: Verification
Re-attempt the questions you failed with 80%+ accuracy required

---

## VERIFICATION GATE

Before bed, you must pass:
1. **Hoisting:** Predict output of 5 hoisting puzzles (5/5)
2. **Event Loop:** Predict order of 3 async code snippets (3/3)
3. **Closures:** Write module, curry, counter from memory (3/3)

If any fail → repeat that section tomorrow.

---

*No new topics until these are solid.*