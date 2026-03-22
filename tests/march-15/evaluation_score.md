# EVALUATION RESULTS | MARCH 15 DAY 3 ASSESSMENT
**Candidate Score: 59/103 (57%)**
**Grade: D (FAIL)**

---

## DETAILED QUESTION-BY-QUESTION EVALUATION

---

## SECTION A: HOISTING - THE TRUTH (20 marks)

### Q1. The Uncomfortable Truth (8 marks)

**Expected:**
```
undefined
ReferenceError: Cannot access 'b' before initialization
ReferenceError: Cannot access 'c' before initialization
```

**Candidate Answer:**
- Undefined
- Error
- Error
- Explanation: "Because of hoisting all the initialisation is on top and for const and let its in tmz so it returns error"

| Part | Expected | Candidate | Marks | Reason |
|------|----------|-----------|-------|--------|
| a) | undefined | undefined | 2 ✅ | Correct |
| b) | ReferenceError | Error | 1.5 ⚠️ | Partial - said "Error" but didn't specify ReferenceError/TDZ |
| c) | ReferenceError | Error | 1.5 ⚠️ | Partial - said "Error" but didn't specify ReferenceError/TDZ |
| Explanation | TDZ, hoisting | TDZ mentioned | 2 ✅ | Adequate explanation |

**Q1 Score: 7/8**

---

### Q2. The If-False Hoisting Trap (6 marks)

**Expected:**
```
undefined
ReferenceError (for y)
undefined
ReferenceError (for y)
```

**Candidate Answer:**
```
Undefined
Undefined
10
Undefined
```

| Part | Expected | Candidate | Marks | Reason |
|------|----------|-----------|-------|--------|
| First x | undefined | Undefined | 1 ✅ | Correct |
| First y | ReferenceError | Undefined | 0 ❌ | WRONG - should be ReferenceError due to TDZ |
| After if x | undefined | 10 | 0 ❌ | WRONG - var hoisted but assignment doesn't run in if(false) |
| After if y | ReferenceError | Undefined | 1 ✅ | Correct |

**Explanation:** "Since var is function scope it goes to the top because of hoisting but for let its block scope and the scope end in if statement" - Partially correct but wrong on key outputs.

**Q2 Score: 2/6**

---

### Q3. Function Hoisting Edge Cases (6 marks)

**Expected:** 5, then TypeError: subtract is not a function

**Candidate Answer:**
- 5 ✅
- "Error since function is passed to variable and function variable is not hoisted" - explains it's an error but incomplete

| Part | Expected | Candidate | Marks | Reason |
|------|----------|-----------|-------|--------|
| add(2,3) | 5 | 5 | 2 ✅ | Correct |
| subtract(5,2) | TypeError | Error | 2 ✅ | Correct - identified error |
| Explanation | Function declarations vs expressions | Mentions variable not hoisted | 2 ⚠️ | Partial - should explain var hoisted but assignment not |

**Q3 Score: 6/6** - Actually correct identification

---

**SECTION A TOTAL: 15/20**

---

## SECTION B: EVENT LOOP - THE EXECUTION ORDER (25 marks)

### Q4. The Race Conditions (10 marks)

**Expected Order:**
1. 1: Start
2. 7: End
3. 3: Promise
4. 4: Microtask
5. 5: Promise Chain
6. 2: Timeout
7. 6: Timeout in Promise

**Candidate Answer:** All 7 correct + explanation

**Q4 Score: 10/10** ✅

---

### Q5. Nested Promise Chaos (8 marks)

**Expected Order:**
1. A: Start
2. F: End
3. B: First then
4. C: Second then
5. D: Nested Promise
6. E: Third then

**Candidate Answer:** All correct + "E prints after d because after then only it prints"

**Q5 Score: 8/8** ✅

---

### Q6. setTimeout in Loop (7 marks)

**Part A (2 marks):** "4 4 4" ✅
**Part B (2 marks):** let fix ✅
**Part C (3 marks):** IIFE attempt - Has issues:
```javascript
for (var i = 1; i <= 3; i++) {  // Starts at 1, should be 0
  (function(x){
    setTimeout(() => {
      console.log(x);
    }, 0);
  })(i);
}
```
- Loop starts at 1, should start at 0 ❌
- Concept of IIFE understood ✅

**Q6 Score: 4/7**

---

**SECTION B TOTAL: 22/25**

---

## SECTION C: CLOSURES - WRITE OR DIE (38 marks)

### Q7. Module Pattern - Bank Account (10 marks)

**Candidate Code:**
```javascript
function createBankAccount(initialBalance) {
  let balance=initialBalance;
  return{
    deposit(amount){
      return balance=balance+amount;
    },
    withdraw(amount){
      If(amount >= 0){  // WRONG! Should be amount > balance
        return "error insufficient fund";
      }else{
        return balance=balance-amount;
      }
    },
    getBalance(){
      return balance;
    },
  }
}
```

**Problems:**
1. `If(amount >= 0)` - INVERTED LOGIC! Should be `amount > balance`
2. With candidate's code, you can NEVER withdraw any money (any amount >= 0 triggers error)
3. Syntax: `If` should be lowercase `if`
4. Missing closing brace for return object

**Expected Outputs vs Candidate Predictions:**
| Test | Expected | Candidate | Marks |
|------|----------|-----------|-------|
| deposit(50) | 150 | 150 | 1 ✅ |
| withdraw(30) | 120 | 120 | 1 ✅ |
| getBalance() | 120 | 120 | 1 ✅ |
| account.balance | undefined | undefined | 1 ✅ |
| withdraw(200) | "Insufficient funds" | "error insufficient fund" | 1 ✅ |

**Q7 Score: 5/10**
- Structure correct: 2 marks
- Outputs mostly correct: 3 marks
- **Critical flaw:** withdraw logic is inverted

---

### Q8. Currying Challenge (12 marks)

**Candidate Code:**
```javascript
function curry(fn) {
  function curriedAdd(...args){
    if( args.length>=fn.length) {  
      fn.apply(this,args)  // MISSING RETURN!
    }   
    return function(...next){
      return curried.apply(this,args.concat(next));
    }
  }
}
```

**Critical Problems:**
1. **MISSING RETURN** before `fn.apply(this,args)` - the function doesn't return the computed result!
2. Hardcoded function name `curriedAdd` instead of using the parameter
3. Broken structure - won't actually work

**Part B:** Redefines the whole function again incorrectly.

**Q8 Score: 2/12**
- Gets partial credit for attempting closure structure
- Code is fundamentally broken - won't work

---

### Q9. Memoization (8 marks)

**Candidate:** LEFT BLANK - No attempt

**Q9 Score: 0/8** ❌

---

### Q10. Stack Implementation (8 marks)

**Candidate Code:**
```javascript
function createStack() {
  let stk=[];
  return {  
    push(item) { return stk.push(item); },
    pop() { return stk.pop(); },
    peek() { return stk.peek(); },  // WRONG!
    size() { return stk.length; },
    isEmpty() { if (stk.length ==0) { return true; } else { return false; } }
  };
}
```

**Problems:**
1. `peek()` calls `stk.peek()` - WRONG! Should be `stk[stk.length-1]`
2. Wrong predictions for outputs

**Expected vs Predicted:**
| Test | Expected | Candidate | Marks |
|------|----------|-----------|-------|
| pop() | 3 | [1,2] | 0 ❌ |
| peek() | 2 | [1,2] | 0 ❌ |
| size | 1 | 2 | 0.5 ❌ |
| pop() | 1 | [1] | 0.5 ❌ |
| pop() | 0 | [] | 0.5 ❌ |
| isEmpty() | true | true | 1 ✅ |

**Q10 Score: 2/8**

---

**SECTION C TOTAL: 9/38**

---

## SECTION D: TYPE COERCION BRUSHUP (10 marks)

### Q11 (2 marks each)

| # | Expected | Candidate | Marks |
|---|----------|-----------|-------|
| a | true | True | 2 ✅ |
| b | false | False | 2 ✅ |
| c | false | False | 2 ✅ |
| d | 0.30000000000000004 | 0.3 | 0 ❌ |
| e | 0 | "[object Object]" | 0 ❌ |

**Q11 Score: 6/10**

---

## SECTION E: SCOPE CHAIN BRUSHUP (10 marks)

### Q12 (10 marks)

**Expected:** 3, 2, 1, 1
**Candidate:** 3, 3, 2, 1

| Output # | Expected | Candidate | Marks |
|----------|----------|-----------|-------|
| 1 (inner) | 3 | 3 | 2.5 ✅ |
| 2 (middle after inner) | 2 | 3 | 0 ❌ |
| 3 (outer after middle) | 1 | 2 | 0 ❌ |
| 4 (global) | 1 | 1 | 2.5 ✅ |

**Q12 Score: 5/10**

---

## FINAL SCORING

| Section | Max | Score |
|---------|-----|-------|
| A: Hoisting | 20 | 15 |
| B: Event Loop | 25 | 22 |
| C: Closures | 38 | 9 |
| D: Type Coercion | 10 | 6 |
| E: Brushup | 10 | 5 |
| **TOTAL** | **103** | **57** |

**Percentage: 55%** (57/103)
**Grade: D (FAIL)**

---

## CRITICAL GAPS STILL PRESENT

### 1. **Hoisting - Q2** (CRITICAL)
- Thought if(false) block doesn't hoist - WRONG
- Var ALWAYS hoists to function scope, regardless of if block

### 2. **Closure Implementation - Q7, Q8, Q9, Q10** (CRITICAL)
- Q7: Inverted withdraw logic - fundamental misunderstanding
- Q8: Missing return statement - broken code
- Q9: Didn't attempt at all
- Q10: peek() wrong implementation

### 3. **Type Coercion - Q11**
- Still wrong on floating point and {} + []

### 4. **Scope Chain - Q12**
- Still confused about which x value is accessed at each level

---

## COMPARISON: DAY 2 vs DAY 3

| Day | Score | Grade |
|-----|-------|-------|
| Day 2 (March 14) | 36% | F |
| Day 3 (March 15) | 57% | D |

**Improvement: +21%** - But still FAILING.

---

## RECOMMENDATION

**DO NOT ADVANCE to new topics.**

The candidate showed improvement (36% → 57%) but:
- Cannot implement working closure code (Section C = 9/38)
- Still has fundamental misunderstandings (hoisting Q2)
- Left entire question blank (Q9)

**Required Action:** 
- Need another day of focused remediation
- Practice WRITING closure code, not just identifying problems
- Must pass 70%+ before advancing

---

*Evaluation complete. Evidence-based marking applied.*