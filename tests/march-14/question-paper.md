# JAVASCRIPT DEEP DIVE | SCOPING, CLOSURES & EXECUTION CONTEXT
**Assessment Date: March 14, 2026**  
**Focus: The Mental Model of JavaScript**  
**Total Marks: 100**  
**Time Allowed: 60 minutes**  

---

> *"JavaScript is easy to learn but hard to master. The difference between junior and senior developers often comes down to one thing: understanding how scope and closures really work."*

---

## WARM-UP: What's the Output? (No explanation needed - just predict)

### Q0. Quick Fire (2 marks each - total 10 marks)

Without running code, predict the output:

```javascript
a) console.log(typeof NaN);

b) console.log(0.1 + 0.2 === 0.3);

c) console.log([] + []);

d) console.log([] + {});

e) console.log({} + []);
```

*Score yourself: 8-10 = warm, 5-7 = OK, 0-4 = Cold start needed*

---

## SECTION A: The Execution Context & Scope Chain (25 marks)

### Q1. Tracing the Scope Chain (10 marks)

You're debugging a tricky bug in production. This code was working yesterday but now prints something unexpected. 

```javascript
var modules = [];

function registerModule(name) {
  var handler = function() {
    console.log("Running module: " + name);
  };
  modules.push(handler);
}

for (var i = 1; i <= 3; i++) {
  registerModule("Module-" + i);
}

modules[0]();
modules[1]();
modules[2]();
```

**Tasks:**
1. What does this actually output? (4 marks)
2. Why is this happening? Explain the scope chain and how `name` is being shared. (4 marks)
3. How would you fix this to output "Module-1", "Module-2", "Module-3"? (2 marks)

---

### Q2. The Shadowing Puzzle (8 marks)

```javascript
var x = "global";

function outer() {
  var x = "outer";
  
  function middle() {
    var x = "middle";
    
    function inner() {
      console.log(x);
    }
    
    inner();
  }
  
  middle();
}

outer();
```

**Question:** What does this print? More importantly - explain the entire scope chain from inner() all the way to global. Why does inner() see "middle" and not "outer" or "global"?

---

### Q3. Hoisting Edge Case (7 marks)

This code was written by a developer who "doesn't use let because it's confusing." Predict what happens:

```javascript
function test() {
  console.log(value);
  
  if (false) {
    var value = "I am never executed";
  }
  
  console.log(value);
}

test();
```

Then explain: Why does this behave this way? What concept in JavaScript causes this?

---

## SECTION B: Closures in the Wild (35 marks)

### Q4. The Module Pattern (12 marks)

You're building a user preferences manager. It should:
- Store user preferences privately
- Expose methods to get/set individual preferences
- Have an "admin" mode that can reset everything
- Prevent direct access to the internal storage

```javascript
// TODO: Implement this
function createPreferencesManager() {
  // Your code here
}

// Expected usage:
const prefs = createPreferencesManager();
prefs.set('theme', 'dark');
prefs.set('language', 'en');
console.log(prefs.get('theme')); // 'dark'

prefs.reset(); // Admin function
console.log(prefs.get('theme')); // Should be reset

// This should NOT work:
console.log(prefs._internalStore); // undefined or error
```

**Tasks:**
1. Implement the function using closures (8 marks)
2. Explain why the internal store is not accessible from outside (4 marks)

---

### Q5. The Classic Closure-in-Loop Bug (10 marks)

This is one of the most common bugs in JavaScript. What happens and how do you fix it?

```javascript
// Scenario: You want to create 3 functions that each log their number
// Expected: f1() logs 1, f2() logs 2, f3() logs 3

var functions = [];

for (var i = 1; i <= 3; i++) {
  functions.push(function() {
    console.log(i);
  });
}

functions[0](); // What does this print?
functions[1](); // What does this print?
functions[2](); // What does this print?
```

**Questions:**
1. What actually prints? Why? (4 marks)
2. Fix this using THREE different approaches (6 marks)
   - Approach 1: Using `let`
   - Approach 2: Using IIFE (Immediately Invoked Function Expression)
   - Approach 3: Using an external factory function

---

### Q6. The Currying Challenge (13 marks)

**Part A (6 marks):** Implement a `curry` function that transforms a multi-argument function into a sequence of single-argument calls.

```javascript
function curry(fn) {
  // Your implementation
  return function curried(...args) {
    // ...
  };
}

// Example:
function add(a, b, c) {
  return a + b + c;
}

const curriedAdd = curry(add);
console.log(curriedAdd(1)(2)(3)); // 6
console.log(curriedAdd(1, 2)(3)); // 6
console.log(curriedAdd(1)(2, 3)); // 6
```

**Part B (7 marks):** Create a `multiplyBy` function that returns a function multiplying its argument by a fixed number:

```javascript
// Define multiplyBy using closures (NOT using curry from above)
function multiplyBy(n) {
  // Your implementation
}

const multiplyBy3 = multiplyBy(3);
console.log(multiplyBy3(10)); // 30
console.log(multiplyBy3(5));  // 15
```

Explain how closures make both currying and multiplyBy possible.

---

## SECTION C: The Execution Order Puzzle (30 marks)

### Q7. Event Loop & Microtasks (15 marks)

Predict the EXACT output order and explain WHY:

```javascript
console.log('1: Start');

setTimeout(() => {
  console.log('2: Timeout');
}, 0);

Promise.resolve()
  .then(() => {
    console.log('3: Promise 1');
  })
  .then(() => {
    console.log('4: Promise 2');
  });

setTimeout(() => {
  console.log('5: Timeout 2');
  
  Promise.resolve()
    .then(() => {
      console.log('6: Promise in Timeout');
    });
}, 0);

console.log('7: End');

/* 
   Your prediction:
   Order: _ _ _ _ _ _ _
*/
```

**Tasks:**
1. Write the exact output order (5 marks)
2. Explain the event loop, macrotask queue, and microtask queue (10 marks)

---

### Q8. Private Data with Closures (15 marks)

Create a function that manages a private counter with the following requirements:

```javascript
function createCounter() {
  // TODO: Implement using closures
  
  // Return an object with:
  // - increment(): increases count by 1, returns new count
  // - decrement(): decreases count by 1, returns new count
  // - getValue(): returns current count
  // - reset(): sets count back to 0
}

// Your implementation here

// Tests:
const counter = createCounter();
console.log(counter.increment()); // ?
console.log(counter.increment()); // ?
console.log(counter.getValue()); // ?
console.log(counter.decrement()); // ?
console.log(counter.reset());    // ?
console.log(counter.getValue()); // ?

// Critical: Can you access count directly?
// console.log(counter.count); // What happens?
```

**Questions:**
1. Implement the function (10 marks)
2. Explain how closures provide true privacy here. What makes this different from using a class with private fields? (5 marks)

---

## BONUS: The Execution Context Deep Dive (+10 marks)

### Q9. What Executes When?

```javascript
var x = 10;

function foo() {
  console.log(x);
}

function bar(fn) {
  var x = 20;
  fn();  // What does this log?
}

bar(foo);  // What is the output?
```

Now explain:
1. What gets logged? (2 marks)
2. Why does it log 10 and not 20? Explain lexical vs dynamic scoping. (4 marks)
3. JavaScript uses lexical scoping. What would dynamic scoping print instead? (2 marks)
4. Why is lexical scoping better for JavaScript? (2 marks)

---

## SCORING GUIDE

| Section | Max Marks | Your Score |
|---------|-----------|------------|
| Warm-up (Q0) | 10 | ___ |
| Section A | 25 | ___ |
| Section B | 35 | ___ |
| Section C | 30 | ___ |
| Bonus (Q9) | +10 | ___ |
| **TOTAL** | **100** | ___ |

| Score | Level | Action |
|-------|-------|--------|
| 90-100 | Ninja | Ready for advanced topics |
| 80-89 | Strong | Minor refinements needed |
| 70-79 | Building | More practice on closures |
| 60-69 | Learning | Review fundamentals again |
| Below 60 | Foundation | Repeat core JS concepts |

---

## REFLECTION (Not graded - think about it)

After completing this test, reflect:
1. Which concept was hardest to reason about?
2. Did you rely on memorization or actual understanding?
3. How would you explain closures to a beginner?

---

*Assessment complete. Return answers for evaluation.*