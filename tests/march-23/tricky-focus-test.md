# TRICKY FOCUS ASSESSMENT
**Date:** March 23, 2026  
**Focus:** Improving attention to detail and identifying subtle intricacies  
**Total Marks:** 100  
**Time Allowed:** 60 minutes  

---

> *"The devil is in the details. What looks complex may be simple if you look closely; what looks simple may hide traps."*  

---

## SECTION A: CODE TRACING & EDGE CASES (30 marks)

### Q1. The Increment Trap (10 marks)
What does this code output?
```javascript
let x = 5;
function foo() {
  let x = 10;
  bar();
  function bar() {
    console.log(x);
  }
}
foo();
```
A) 5  
B) 10  
C) undefined  
D) ReferenceError

### Q2. The Slice & Splice Switcheroo (10 marks)
What is the final state of `arr`?
```javascript
let arr = [1, 2, 3, 4, 5];
let part = arr.slice(1, 4);
part[0] = 99;
arr.splice(2, 1, part);
console.log(arr);
```
A) [1, 2, [99, 3, 4], 4, 5]  
B) [1, 2, 99, 3, 4, 4, 5]  
C) [1, 2, [99, 3, 4], 5]  
D) [1, 2, 99, 3, 4, 5]

### Q3. The Async Illusion (10 marks)
What is the exact output order?
```javascript
console.log('start');
setTimeout(() => console.log('timeout'), 0);
Promise.resolve().then(() => console.log('promise'));
queueMicrotask(() => console.log('microtask'));
console.log('end');
```
Write the sequence (e.g., start, end, microtask, promise, timeout).

---

## SECTION B: SUBTLE BUG DETECTION (30 marks)

### Q4. The Off-by-One That Isn't (10 marks)
This function is supposed to return the sum of array elements. What's wrong?
```javascript
function sumArray(arr) {
  let sum = 0;
  for (let i = 0; i <= arr.length; i++) {
    sum += arr[i];
  }
  return sum;
}
```
A) Correct implementation  
B) Will cause ReferenceError for empty array  
C) Will skip the last element  
D) Will cause undefined addition on last iteration

### Q5. The Closure That Forgot (10 marks)
Why does this not work as expected?
```javascript
function createFunctions() {
  let funcs = [];
  for (var i = 0; i < 3; i++) {
    funcs[i] = function() {
      return i * 2;
    };
  }
  return funcs;
}

let fns = createFunctions();
console.log(fns[0](), fns[1](), fns[2]());
```
A) Returns 0, 2, 4  
B) Returns 6, 6, 6  
C) Returns undefined, undefined, undefined  
D) Returns 0, 0, 0

### Q6. The Recursive Base Case Blind Spot (10 marks)
This factorial function works for most inputs but fails on one critical case. Which?
```javascript
function factorial(n) {
  if (n === 1) {
    return 1;
  }
  return n * factorial(n - 1);
}
```
A) Works for all positive integers  
B) Returns NaN for n=0  
C) Causes stack overflow for n=0  
D) Returns 0 for n=1

---

## SECTION C: PATTERN RECOGNITION & TRICKY QUESTIONS (40 marks)

### Q7. The Twin Array Switch (10 marks)
Given:
```javascript
let a = [1, 2, 3];
let b = a;
b[0] = 99;
```
What are `a` and `b` after execution?
A) a=[1,2,3], b=[99,2,3]  
B) a=[99,2,3], b=[99,2,3]  
C) a=[1,2,3], b=[1,2,3]  
D) a=[99,2,3], b=[1,2,3]

### Q8. The Argument That Isn't (10 marks)
What does this log?
```javascript
function mystery(x, y) {
  arguments[0] = 10;
  arguments[1] = 20;
  console.log(x, y);
}
mystery(1, 2);
```
A) 1 2  
B) 10 20  
C) 10 2  
D) 20 10

### Q9. The Filter That Changes Length (10 marks)
What does this output?
```javascript
let arr = [1, 2, 3, 4, 5];
let result = arr.filter((val, idx) => {
  if (val % 2 === 0) {
    arr.push(val + 10);
  }
  return val % 2 === 0;
});
console.log(result.length);
```
A) 2  
B) 3  
C) 4  
D) Infinite loop / never finishes

### Q10. The Object Key Coercion (10 marks)
What is printed?
```javascript
let obj = {};
obj[0] = 'zero';
obj[1] = 'one';
obj[true] = 'boolTrue';
obj[false] = 'boolFalse';
obj[null] = 'null';
obj[undefined] = 'undefined';
console.log(obj[0], obj[1], obj[true], obj[false], obj[null], obj[undefined]);
```
A) zero one boolTrue boolFalse null undefined  
B) zero one true false null undefined  
C) zero one true false undefined undefined  
D) zero one true false undefined null

---

## SCORING GUIDE
- Each question: 10 marks
- No partial credit for multiple choice unless work shown indicates correct reasoning
- Coding questions: correct answer gets full points; explanation may earn partial if approach is right but answer wrong

**Instructions:**
1. Read each question carefully—look for the twist.
2. If a question seems impossible, re-read for hidden simplicity.
3. If a question seems trivial, double-check for traps.
4. Check your work if time permits.

---
*When finished, compare your answers to the key to see where your focus served you—and where it slipped.*