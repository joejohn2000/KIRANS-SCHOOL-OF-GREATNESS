# ANSWER KEY | DAY 3 ASSESSMENT - MARCH 15

---

## SECTION A: HOISTING - THE TRUTH (20 marks)

### Q1. The Uncomfortable Truth (8 marks)

```javascript
function test() {
  console.log(a);  // undefined
  console.log(b);  // ReferenceError: Cannot access 'b' before initialization
  console.log(c);  // ReferenceError: Cannot access 'c' before initialization
  
  var a = 1;
  let b = 2;
  const c = 3;
}
```

**Answer:** 
```
undefined
ReferenceError: Cannot access 'b' before initialization
ReferenceError: Cannot access 'c' before initialization
```

**Why:**
- `var a` is hoisted and initialized to `undefined`
- `let b` and `const c` are hoisted but NOT initialized (Temporal Dead Zone)
- Accessing them before declaration throws ReferenceError

---

### Q2. The If-False Hoisting Trap (6 marks)

```javascript
function weird() {
  console.log(x);  // undefined
  console.log(y);  // ReferenceError: Cannot access 'y' before initialization
  
  if (false) {
    var x = 10;
    let y = 20;
  }
  
  console.log(x);  // undefined
  console.log(y);  // ReferenceError: Cannot access 'y' before initialization
}
```

**Answer:**
```
undefined
ReferenceError
undefined
ReferenceError
```

**Why:**
- `var` is hoisted to function scope, regardless of if block
- Even `if (false)` still hoists the var declaration
- `let` in the if block is still in TDZ because we never enter the block

---

### Q3. Function Hoisting Edge Cases (6 marks)

```javascript
console.log(add(2, 3));      // 5
console.log(subtract(5, 2));  // TypeError: subtract is not a function

function add(a, b) {
  return a + b;
}

var subtract = function(a, b) {
  return a - b;
};
```

**Answer:** `5`, then `TypeError: subtract is not a function`

**Why:**
- Function declarations are fully hoisted (name + body)
- Variable declarations are hoisted, but assignments are NOT
- `var subtract = function...` becomes: `var subtract;` (undefined), then assignment
- When called, `subtract` is `undefined`, so calling it throws TypeError

---

## SECTION B: EVENT LOOP - THE EXECUTION ORDER (25 marks)

### Q4. The Race Conditions (10 marks)

```javascript
console.log('1: Start');           // 1. Sync
setTimeout(() => console.log('2: Timeout'), 0);  // Macrotask
Promise.resolve().then(() => console.log('3: Promise'));  // Microtask
queueMicrotask(() => console.log('4: Microtask'));  // Microtask
Promise.resolve()
  .then(() => {
    console.log('5: Promise Chain');
    setTimeout(() => console.log('6: Timeout in Promise'), 0);
  });
console.log('7: End');
```

**Exact Order:**
```
1: Start
7: End
3: Promise
4: Microtask
5: Promise Chain
2: Timeout
6: Timeout in Promise
```

**Why:**
1. Sync code runs first: 1, 7
2. Check microtask queue (before macrotasks): 3, 4, 5
3. After microtasks done: first macrotask (2)
4. Inside 2, new microtask added: 6
5. Process microtasks: 6
6. Done

---

### Q5. Nested Promise Chaos (8 marks)

```javascript
console.log('A: Start');
// ... promises ...
console.log('F: End');
```

**Exact Order:**
```
A: Start
F: End
B: First then
C: Second then
D: Nested Promise
E: Third then
```

**Why:**
- A, F run synchronously
- Then microtasks run: B runs, returns 'B-return'
- C's then runs (because B returned), prints C, queues nested promise
- D is a microtask, runs before E
- E runs after D completes

---

### Q6. setTimeout in Loop (7 marks)

**Part A:** `3, 3, 3` (var is shared)

**Part B - Fix with let:**
```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
// Output: 0, 1, 2
```

**Part C - Fix with IIFE:**
```javascript
for (var i = 0; i < 3; i++) {
  (function(i) {
    setTimeout(() => console.log(i), 0);
  })(i);
}
// Output: 0, 1, 2
```

---

## SECTION C: CLOSURES - WRITE OR DIE (35 marks)

### Q7. The Module Pattern (10 marks)

```javascript
function createBankAccount(initialBalance) {
  var balance = initialBalance;  // Private
  
  return {
    deposit: function(amount) {
      balance += amount;
      return balance;
    },
    withdraw: function(amount) {
      if (amount > balance) {
        return 'Insufficient funds';
      }
      balance -= amount;
      return balance;
    },
    getBalance: function() {
      return balance;
    }
  };
}
```

**Outputs:**
```
150  // deposit(50)
120  // withdraw(30)
120  // getBalance()
undefined  // account.balance
Insufficient funds  // withdraw(200)
```

---

### Q8. The Currying Challenge (12 marks)

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

**This is the ONLY correct answer** - hardcoded versions get 0 marks.

**How it works:**
- `fn.length` gives the number of parameters the original function expects
- When enough arguments are collected (`args.length >= fn.length`), call the original function
- Otherwise, return a new function that collects more arguments
- Use closure to "remember" the accumulated arguments across calls

---

### Q9. Memoization (8 marks)

```javascript
function memoize(fn) {
  var cache = {};
  
  return function(...args) {
    var key = args.join(',');
    if (cache.hasOwnProperty(key)) {
      return cache[key];
    }
    var result = fn.apply(this, args);
    cache[key] = result;
    return result;
  };
}
```

---

### Q10. The Private Class Pattern (8 marks)

```javascript
function createStack() {
  var items = [];  // Private array
  
  return {
    push: function(item) {
      items.push(item);
    },
    pop: function() {
      return items.pop();
    },
    peek: function() {
      return items[items.length - 1];
    },
    isEmpty: function() {
      return items.length === 0;
    },
    get size() {
      return items.length;
    }
  };
}
```

**Note:** Can't truly make `size` read-only without Object.defineProperty, but this works for the test.

---

## SECTION D: TYPE COERCION BRUSHUP (10 marks)

### Q11.

```javascript
a) [] == false;       // true  ([] coerces to "", then to 0, false is 0)
b) [] === false;      // false (different types)
c) ![];               // false ([] is truthy, ![] is false)
d) 0.1 + 0.2;        // 0.30000000000000004 (floating point)
e) {} + [];           // 0  ({} is empty block, +[] is 0)
```

---

## SECTION E: BRUSHUP (10 marks)

### Q12.

```javascript
// Outputs in order:
3  // inner() - sees middle's x
2  // middle() after inner - sees outer's x  
1  // outer() after middle - sees global's x (shadowed)
1  // global after all - sees global x
```

---

## SCORING

| Section | Max | Your Score |
|---------|-----|------------|
| A: Hoisting | 20 | ___ |
| B: Event Loop | 25 | ___ |
| C: Closures | 38 | ___ |
| D: Type Coercion | 10 | ___ |
| E: Brushup | 10 | ___ |
| **TOTAL** | **103** | ___ |

**To convert to 100%: (Score ÷ 103) × 100 = ___%**

---

*End of Answer Key*