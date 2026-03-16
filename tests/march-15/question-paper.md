# DAY 3 ASSESSMENT | JAVASCRIPT FUNDAMENTALS DEEP DIVE
**Assessment Date: March 15, 2026**
**Focus: Hoisting, Event Loop, Closures & Type Coercion**
**Total Marks: 100**
**Time Allowed: 60 minutes**

---

> *"Yesterday you failed. Today you either fix it or you don't. Simple."*

---

## SECTION A: HOISTING - THE TRUTH (20 marks)

### Q1. The Uncomfortable Truth (8 marks)

```javascript
function test() {
  console.log(a);
  console.log(b);
  console.log(c);
  
  var a = 1;
  let b = 2;
  const c = 3;
}

test();
```

**Write the exact output. Then explain WHY.**

---

### Q2. The If-False Hoisting Trap (6 marks)

```javascript
function weird() {
  console.log(x);
  console.log(y);
  
  if (false) {
    var x = 10;
    let y = 20;
  }
  
  console.log(x);
  console.log(y);
}

weird();
```

**What does this print? Why does `var` behave this way even inside an if(false)?**

---

### Q3. Function Hoisting Edge Cases (6 marks)

```javascript
console.log(add(2, 3));
console.log(subtract(5, 2));

function add(a, b) {
  return a + b;
}

var subtract = function(a, b) {
  return a - b;
};
```

**Explain what prints and why. What is the difference between function declarations and function expressions?**

---

## SECTION B: EVENT LOOP - THE EXECUTION ORDER (25 marks)

### Q4. The Race Conditions (10 marks)

```javascript
console.log('1: Start');

setTimeout(() => console.log('2: Timeout'), 0);

Promise.resolve()
  .then(() => console.log('3: Promise'));

queueMicrotask(() => console.log('4: Microtask'));

Promise.resolve()
  .then(() => {
    console.log('5: Promise Chain');
    setTimeout(() => console.log('6: Timeout in Promise'), 0);
  });

console.log('7: End');

/*
  PREDICT THE EXACT ORDER:
  _ : _
  _ : _
  _ : _
  _ : _
  _ : _
  _ : _
  _ : _
*/
```

**Write the exact 7-line output in order. Then explain WHY each step happens.**

---

### Q5. Nested Promise Chaos (8 marks)

```javascript
console.log('A: Start');

Promise.resolve()
  .then(() => {
    console.log('B: First then');
    return 'B-return';
  })
  .then(() => {
    console.log('C: Second then');
    Promise.resolve()
      .then(() => console.log('D: Nested Promise'));
  })
  .then(() => console.log('E: Third then'));

console.log('F: End');

/*
  ORDER: _ _ _ _ _ _
*/
```

**Predict exact output. When does 'E' print - before or after 'D'? Why?**

---

### Q6. setTimeout in Loop (7 marks)

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}

// What logs? Then fix it to print 0, 1, 2
```

**Part A:** What actually prints? (2 marks)  
**Part B:** Fix using let (2 marks)  
**Part C:** Fix using IIFE (3 marks)

---

## SECTION C: CLOSURES - WRITE OR DIE (35 marks)

### Q7. The Module Pattern - IMPLEMENT (9 marks)

**Write a complete working implementation:**

```javascript
function createBankAccount(initialBalance) {
  // TODO: Implement
  
  // Requirements:
  // - Private balance variable
  // - deposit(amount) - returns new balance
  // - withdraw(amount) - returns new balance (or error if insufficient)
  // - getBalance() - returns current balance
  // - Cannot access balance directly (account.balance should be undefined)
}

// Tests:
const account = createBankAccount(100);
console.log(account.deposit(50));      // ?
console.log(account.withdraw(30));      // ?
console.log(account.getBalance());      // ?
console.log(account.balance);           // ?
console.log(account.withdraw(200));     // ?
```

---

### Q8. The Currying Challenge - IMPLEMENT (10 marks)

**Write a GENERAL curry function (not hardcoded):**

```javascript
function curry(fn) {
  // Your implementation
}

// MUST work for ANY number of arguments:
const add = (a, b, c, d) => a + b + c + d;
const curriedAdd = curry(add);

console.log(curriedAdd(1)(2)(3)(4));     // 10
console.log(curriedAdd(1, 2)(3)(4));     // 10
console.log(curriedAdd(1, 2, 3)(4));    // 10
console.log(curriedAdd(1)(2, 3, 4));    // 10
```

**Then use your curry to create:**
```javascript
const multiply = (a, b, c) => a * b * c;
const curriedMultiply = curry(multiply);

const multiplyBy2 = curriedMultiply(2);  // function that multiplies by 2
console.log(multiplyBy2(3)(4));          // 24
```

---

### Q9. Memoization - IMPLEMENT (8 marks)

```javascript
function memoize(fn) {
  // Your implementation
}

// Tests:
let callCount = 0;
function expensive(a, b) {
  callCount++;
  return a + b;
}

const memoized = memoize(expensive);

console.log(memoized(2, 3));  // 5, callCount = 1
console.log(memoized(2, 3));  // 5, callCount = 1 (cached!)
console.log(memoized(4, 5));  // 9, callCount = 2
console.log(memoized(4, 5));  // 9, callCount = 2 (cached!)
```

---

### Q10. The Private Class Pattern (8 marks)

```javascript
function createStack() {
  // Implement using closures (NOT classes)
  // Requirements:
  // - push(item) - add to stack
  // - pop() - remove and return last item
  // - peek() - see last item without removing
  // - isEmpty() - boolean
  // - size - read-only property (how?)

  return {
    // Your code
  };
}

// Tests:
const stack = createStack();
stack.push(1);
stack.push(2);
stack.push(3);
console.log(stack.pop());     // ?
console.log(stack.peek());    // ?
console.log(stack.size);      // ?
console.log(stack.pop());     // ?
console.log(stack.pop());     // ?
console.log(stack.isEmpty()); // ?
```

---

## SECTION D: TYPE COERCION BRUSHUP (10 marks)

### Q11. What Actually Happens? (10 marks - 2 each)

```javascript
a) console.log([] == false);

b) console.log([] === false);

c) console.log(![]);

d) console.log(0.1 + 0.2);

e) console.log({} + []);
```

**Predict each output. Explain WHY.**

---

## SECTION E: BRUSHUP - SCOPE CHAIN (10 marks)

### Q12. Quick Scope Check (10 marks)

```javascript
var x = 1;

function outer() {
  var x = 2;
  
  function middle() {
    var x = 3;
    
    function inner() {
      console.log(x);  // What prints?
    }
    
    inner();
    console.log(x);   // What prints?
  }
  
  middle();
  console.log(x);     // What prints?
}

outer();
console.log(x);       // What prints?
```

**Give all 4 outputs. This is a free one if you got Q2 right yesterday.**

---

## SCORING

| Section | Max | Score |
|---------|-----|-------|
| A: Hoisting | 20 | ___ |
| B: Event Loop | 25 | ___ |
| C: Closures | 35 | ___ |
| D: Type Coercion | 10 | ___ |
| E: Brushup | 10 | ___ |
| **TOTAL** | **100** | ___ |


---

## GRADE THRESHOLDS

| Score | Grade | Action |
|-------|-------|--------|
| 90-100 | A | Ready for advanced topics |
| 80-89 | B | Minor gaps, close them |
| 70-79 | C | More practice needed |
| 60-69 | D | Serious gaps remain |
| Below 60 | F | Repeat remediation |

---

*This test separates those who understand from those who memorized. Good luck.*