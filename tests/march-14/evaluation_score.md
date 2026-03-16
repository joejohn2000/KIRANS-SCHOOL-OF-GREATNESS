# EVALUATION RESULTS | MARCH 14 JAVASCRIPT ASSESSMENT
**Candidate Score: 36/100 (36%)**
**Grade: F (FAIL)**

---

## DETAILED MARKING

---

## WARM-UP: Quick Fire (10 marks)

| # | Question | Correct Answer | Candidate Answer | Marks |
|---|----------|---------------|------------------|-------|
| a | typeof NaN | "number" | "number" | 2 ✅ |
| b | 0.1 + 0.2 === 0.3 | false | "True" | 0 ❌ |
| c | [] + [] | "" (empty string) | " " | 1 ⚠️ |
| d | [] + {} | "[object Object]" | "[object Object]" | 2 ✅ |
| e | {} + [] | 0 | "[object Object]" | 0 ❌ |

**Warm-up Score: 5/10**

---

## SECTION A: The Execution Context & Scope Chain (25 marks)

### Q1: Tracing the Scope Chain (10 marks)

| Part | Expected | Candidate | Marks |
|------|----------|-----------|-------|
| 1. Output | Module-4 (all 3 times) | "Running module: Module-4" x3 | 4 ✅ |
| 2. Explanation | var is function-scoped, shared reference | "Var is function scope so it cannot store the variable in a block like for. Name is shared by call by reference" | 4 ✅ |
| 3. Fix | Use let or IIFE | "We can fix this by using let instead of var" | 2 ✅ |

**Q1 Score: 10/10**

---

### Q2: The Shadowing Puzzle (8 marks)

| Expected | Candidate | Marks |
|----------|-----------|-------|
| Output: "middle" | "Middle" | 3 ✅ |
| LEGB rule explanation | "it has given output middle because of the legb rule which means first it takes local variable after that enclosing variables..." | 5 ✅ |

**Q2 Score: 8/8**

---

### Q3: Hoisting Edge Case (7 marks)

| Expected | Candidate | Marks |
|----------|-----------|-------|
| Output: undefined, undefined | "This returns error because var is function scoped and not block scope so the scope of var value = 'I am never executed'; stays in the block only" | 0 ❌ |

**CRITICAL FAILURE:** Candidate does NOT understand hoisting. The code does NOT return an error - it prints `undefined` twice because `var` declarations are hoisted and initialized to `undefined`.

**Q3 Score: 0/7**

---

**Section A Total: 18/25**

---

## SECTION B: Closures in the Wild (35 marks)

### Q4: The Module Pattern (12 marks)

| Expected | Candidate | Marks |
|----------|-----------|-------|
| Full implementation with get/set/reset | "Return {" with no implementation + "Internal store does not work because of lack of permission" | 0 ❌ |

**CRITICAL FAILURE:** Candidate did NOT implement anything. The code is empty/incomplete. The explanation about "lack of permission" shows fundamental misunderstanding - it's about scope, not permissions.

**Q4 Score: 0/12**

---

### Q5: The Classic Closure-in-Loop Bug (10 marks)

| Part | Expected | Candidate | Marks |
|------|----------|-----------|-------|
| 1. Output | 4, 4, 4 | 4, 4, 4 | 3 ✅ |
| 2. Three fixes | let, IIFE, factory | let ✅, var with param (but wrong) ❌, let j=i (syntax error) ❌ | 1/3 |

Candidate's fixes:
- Fix 1: Using let ✅
- Fix 2: `for (var i = 1; i <= 3; i++) { functions.push(function(k) { console.log(k); }); }` - WRONG. The parameter `k` is never passed.
- Fix 3: `for (var i = 1; i <= 3; i++) { Let j=i ...` - SYNTAX ERROR, incomplete

**Q5 Score: 4/10**

---

### Q6: The Currying Challenge (13 marks)

**Part A (6 marks):**

| Expected | Candidate | Marks |
|----------|-----------|-------|
| General curry for any function | Hardcoded for exactly 3 args | 0 ❌ |

Candidate wrote:
```javascript
function curried(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    };
  };
}
```

This ONLY works for 3-argument functions. Cannot handle:
- `curriedAdd(1, 2)(3)` - Would fail
- `curriedAdd(1)(2, 3)` - Would fail

**Part Score: 0/6**

---

**Part B (7 marks):**

| Expected | Candidate | Marks |
|----------|-----------|-------|
| `function multiplyBy(n) { return function(x) { return n * x; }; }` | `return n*3;` | 0 ❌ |

Candidate wrote: `return n*3;`

This is COMPLETELY WRONG:
- `multiplyBy(3)` returns `9` (a number)
- `multiplyBy3(10)` would be `9(10)` - calling a number as a function = CRASH

**Part Score: 0/7**

---

**Q6 Total: 0/13**

---

**Section B Total: 4/35**

---

## SECTION C: The Execution Order Puzzle (30 marks)

### Q7: Event Loop & Microtasks (15 marks)

| Expected Output Order | Candidate's Answer | Marks |
|----------------------|--------------------|-------|
| 1. 1: Start | 1: Start | ✅ |
| 2. 7: End | 2: Timeout | ❌ |
| 3. 3: Promise 1 | 5: Timeout 2 | ❌ |
| 4. 4: Promise 2 | 6: Promise 1 | ❌ |
| 5. 2: Timeout | 7: End | ❌ |
| 6. 5: Timeout 2 | 3: Promise 1 | ❌ |
| 7. 6: Promise in Timeout | 4: Promise 1 | ❌ |

**COMPLETELY WRONG ORDER.** Candidate does NOT understand the event loop at all.

Explanation: "started in begin as its in the top of the code" - shows fundamental misunderstanding.

**Q7 Score: 0/15**

---

### Q8: Private Data with Closures (15 marks)

| Expected | Candidate | Marks |
|----------|-----------|-------|
| increment: returns 1, 2 | increment: returns 1, 2 | 2 ✅ |
| getValue: returns 2 | getValue: returns 2 | 1 ✅ |
| decrement: returns 1 | decrement: returns 1 | 1 ✅ |
| reset: returns 0 | reset: returns 0 | 0 ❌ |
| getValue: returns 0 | getValue: returns 0 | 0 ❌ |
| Privacy explanation | "Closure acts as a backpack. It remembers the values stored in data in the scope only. So it is more secure" | 0 ❌ |

Candidate's code:
```javascript
return {
  increment: function() { currentValue += 1; },
  decrement: function() { currentValue -= 1; },
  getValue: function() { return currentValue; }
  reset: function() {   // MISSING COMMA!
    return 0;
  }
};
```

Problems:
1. Missing comma after getValue - syntax error
2. reset() doesn't actually reset the variable - it just returns 0 without updating currentValue
3. The privacy explanation is vague ("backpack") - doesn't explain WHY it's private

**Q8 Score: 4/15**

---

**Section C Total: 4/30**

---

## BONUS: Execution Context Deep Dive (10 marks)

### Q9

| Part | Expected | Candidate | Marks |
|------|----------|-----------|-------|
| 1. Output | 10 | 10 | 2 ✅ |
| 2. Lexical vs Dynamic | Lexical scoping - defined where written, not called | "It got 10 because its enclosing variable is 10" | 3 ✅ |
| 3. Dynamic would print | 20 | (blank) | 0 ❌ |
| 4. Why lexical better | Predictable, enables closures | (blank) | 0 ❌ |

**Q9 Score: 5/10**

---

## FINAL SCORING

| Section | Max | Score |
|---------|-----|-------|
| Warm-up | 10 | 5 |
| Section A | 25 | 18 |
| Section B | 35 | 4 |
| Section C | 30 | 4 |
| Bonus | 10 | 5 |
| **TOTAL** | **110** | **36** |

**Converted to 100: 36/100 (36%)**

---

## GRADE: F (FAIL)

---

## CRITICAL GAPS IDENTIFIED

### 1. Hoisting (Q3 - 0/7)
- **Issue:** Candidate thinks hoisting causes errors
- **Reality:** var declarations are hoisted and initialized to `undefined`
- **Fix:** Study hoisting deeply - declarations vs assignments

### 2. Event Loop (Q7 - 0/15)
- **Issue:** Complete misunderstanding of microtasks vs macrotasks
- **Reality:** Promises go to microtask queue (runs BEFORE setTimeout)
- **Fix:** Study the event loop, microtask queue, macrotask queue

### 3. Closures - Cannot Implement (Q4, Q6, Q8)
- **Issue:** Cannot write working closure-based code
- **Reality:** Can identify problems but cannot solve them
- **Fix:** Practice writing closure-based utilities from scratch

### 4. Curry Implementation (Q6)
- **Issue:** Hardcoded for 3 arguments only
- **Reality:** Not a general solution
- **Fix:** Study how to track accumulated arguments

### 5. Module Pattern (Q4)
- **Issue:** Completely empty implementation
- **Reality:** Cannot translate concept to code
- **Fix:** Practice the revealing module pattern

---

## RECOMMENDATION

**DO NOT ADVANCE to new topics.**

The candidate demonstrates:
- ✅ Can identify problems (Q1, Q2, Q5 output)
- ❌ Cannot implement solutions (Q4, Q6, Q8)
- ❌ Does not understand fundamental concepts (hoisting, event loop)

**Required Action:** Repeat JavaScript fundamentals with heavy emphasis on:
1. Writing closure-based code (daily practice)
2. Understanding hoisting in depth
3. Event loop and async execution
4. Implementing patterns (module, curry, memoize)

This is a foundational issue that will block all future learning if not addressed.

---

*Evaluation complete.*