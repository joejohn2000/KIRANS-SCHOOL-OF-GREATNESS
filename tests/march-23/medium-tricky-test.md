# MEDIUM TRICKY FOCUS ASSESSMENT
**Date:** March 23, 2026  
**Focus:** Medium difficulty questions targeting attention to detail and implementation accuracy  
**Total Marks:** 100  
**Time Allowed:** 60 minutes  

---

> *"Focus is not just about concentration—it's about knowing where to look and what details matter."*  

---

## SECTION APPEARANCE VS REALITY (25 marks)

### Q1. The Deceptive Loop (8 marks)
What does this code actually output? (Trace it carefully!)
```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// What prints immediately after this loop runs?
```
A) 0, 1, 2 (after 100ms)  
B) 3, 3, 3 (after 100ms)  
C) 0, 1, 2 (immediately)  
D) Nothing prints

### Q2. The Array That Lies (8 marks)
What is the length of the resulting array?
```javascript
let arr = [1, 2, 3, 4, 5];
arr[10] = 99;
console.log(arr.length);
```
A) 5  
B) 6  
C) 11  
D) 10

### Q3. The Function That Forgets (9 marks)
What does this output?
```javascript
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}
let add5 = makeAdder(5);
let add10 = makeAdder(10);
console.log(add5(3), add10(3));
```
A) 8 13  
B) 8 8  
C) 13 13  
D) 5 10

---

## SECTION B: EDGE CASE MASTERY (25 marks)

### Q4. The Empty Array Trap (8 marks)
What does this return for an empty array?
```javascript
function getMax(arr) {
  return Math.max(...arr);
}
console.log(getMax([]));
```
A) 0  
B) -Infinity  
C) NaN  
D) Error

### Q5. The Off-by-One Illusion (8 marks)
This function is supposed to check if a number is prime. For which input does it fail?
```javascript
function isPrime(n) {
  if (n < 2) return false;
  for (let i = 2; i < n; i++) {
    if (n % i === 0) return false;
  }
  return true;
}
```
A) n = 0  
B) n = 1  
C) n = 2  
D) n = 4

### Q6. The String That's Not (9 marks)
What does this output?
```javascript
let str = "hello";
str[0] = "H";
console.log(str);
```
A) "Hello"  
B) "hello"  
C) "H"  
D) TypeError

---

## SECTION C: IMPLEMENTATION PRECISION (25 marks)

### Q7. The Switch That Slips (8 marks)
What does this output?
```javascript
let x = 1;
switch (x) {
  case 1:
    console.log("one");
  case 2:
    console.log("two");
  default:
    console.log("default");
}
```
A) "one"  
B) "one" "two" "default"  
C) "two" "default"  
D) "default"

### Q8. The Parameters That Shift (8 marks)
What does this output?
```javascript
function test(a, b = 1) {
  console.log(a, b);
}
test(5);
```
A) 5 1  
B) 5 undefined  
C) undefined 1  
D) Error

### Q9. The Return That Forgets (9 marks)
What does this function return for input [1,2,3]?
```javascript
function doubleValues(arr) {
  arr.forEach((val, idx) => {
    arr[idx] = val * 2;
  });
  return arr;
}
console.log(doubleValues([1,2,3]));
```
A) [2,4,6]  
B) [1,2,3]  
C) undefined  
D) [2,4,6, undefined, undefined, undefined]

---

## SECTION D: PATTERN RECOGNITION UNDER PRESSURE (25 marks)

### Q10. The Nested Scope Switch (8 marks)
What does this output?
```javascript
let x = "global";
function outer() {
  let x = "outer";
  function inner() {
    let x = "inner";
    console.log(x);
  }
  inner();
  console.log(x);
}
outer();
console.log(x);
```
A) inner outer global  
B) outer outer global  
C) inner inner inner  
D) global global global

### Q11. The Async Microtask Maze (9 marks)
What is the exact output?
```javascript
console.log('start');
setTimeout(() => console.log('timeout1'), 0);
Promise.resolve().then(() => console.log('promise1'));
queueMicrotask(() => console.log('microtask1'));
Promise.resolve().then(() => {
  console.log('promise2');
  setTimeout(() => console.log('timeout2'), 0);
});
console.log('end');
```
Write the exact sequence.

### Q12. The Recursive Window (8 marks)
What does this return for n=4?
```javascript
function mystery(n) {
  if (n <= 0) return 0;
  if (n % 2 === 0) {
    return n + mystery(n - 1);
  } else {
    return mystery(n - 1);
  }
}
console.log(mystery(4));
```
A) 4  
B) 6  
C) 10  
D) 16

---

## SCORING GUIDE
- Questions 1-3: 8 marks each (24 total)
- Questions 4-6: 8 marks each (24 total)  
- Questions 7-9: 8 marks each (24 total)
- Questions 10-12: 8-9 marks each (25 total)
- Total: 100 marks

**Instructions:**
1. These questions are designed to test your focus—look for where the apparent simplicity or complexity hides the real behavior.
2. If a question seems too easy, you've likely missed a detail.
3. If a question seems impossible, break it down step by step.
4. Pay special attention to edge cases, boundary conditions, and subtle language behaviors.
5. Check your work if time permits.

---
*When finished, review your answers carefully. The questions that felt "tricky" are exactly where your focus needs sharpening.*