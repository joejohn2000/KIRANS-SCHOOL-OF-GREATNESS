# DAY 22 ASSESSMENT | DAYS 1-7 REVIEW
**Assessment Date: March 22, 2026**  
**Focus: Review of Days 1-7 Fundamentals**  
**Total Marks: 100**  
**Time Allowed: 60 minutes**  

---

> *"Review what you've learned so far to build a strong foundation."*

---

## SECTION A: BIG O COMPLEXITY (DAY 3) (20 marks)

### Q1. Time Complexity Analysis (8 marks)
What is the time complexity of this code?
```javascript
function findMax(arr) {
  let max = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
  }
  return max;
}
```
A) O(1)  
B) O(n)  
C) O(n²)  
D) O(log n)

### Q2. Space Complexity (6 marks)
What is the space complexity of the findMax function above?
A) O(1)  
B) O(n)  
C) O(n²)  
D) O(log n)

### Q3. Nested Loops (6 marks)
What is the time complexity of this code?
```javascript
function hasDuplicate(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] === arr[j]) {
        return true;
      }
    }
  }
  return false;
}
```
A) O(1)  
B) O(n)  
C) O(n²)  
D) O(log n)

---

## SECTION B: ARRAY/LIST OPERATIONS (DAY 4) (20 marks)

### Q4. Array Methods (8 marks)
What will this code output?
```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(x => x * 2);
const evens = doubled.filter(x => x % 2 === 0);
const sum = evens.reduce((acc, x) => acc + x, 0);
console.log(sum);
```
A) 12  
B) 24  
C) 30  
D) 36

### Q5. Two-Pointer Technique (6 marks)
Which problem is BEST solved using the two-pointer technique?
A) Finding if an array contains a specific value  
B) Finding two numbers in a sorted array that add up to a target  
C) Calculating the sum of all elements in an array  
D) Reversing an array

### Q6. Array Transformation (6 marks)
Write a function that takes an array and returns a new array with each element squared:
```javascript
function squareArray(arr) {
  // Your code here
}
// squareArray([1, 2, 3]) should return [1, 4, 9]
```

---

## SECTION C: DICTIONARIES/HASH MAPS (DAY 5) (20 marks)

### Q7. Hash Map Usage (8 marks)
What will this code output?
```javascript
const counts = {};
const letters = ['a', 'b', 'a', 'c', 'b', 'a'];
for (const letter of letters) {
  counts[letter] = (counts[letter] || 0) + 1;
}
console.log(counts['a']);
```
A) 1  
B) 2  
C) 3  
D) 4

### Q8. When to Use Hash Maps (6 marks)
Hash maps are MOST useful for:
A) Storing ordered data  
B) When you need fast lookups by key  
C) When you need to maintain insertion order  
D) When you need to store duplicate keys

### Q9. Frequency Counter (6 marks)
Write a function that returns the most frequent element in an array:
```javascript
function mostFrequent(arr) {
  // Your code here
}
// mostFrequent([1, 2, 2, 3, 3, 3]) should return 3
```

---

## SECTION D: RECURSION (DAY 6) (20 marks)

### Q10. Recursive Factorial (8 marks)
What will this code output?
```javascript
function factorial(n) {
  if (n === 0) {
    return 1;
  }
  return n * factorial(n - 1);
}
console.log(factorial(4));
```
A) 4  
B) 6  
C) 12  
D) 24

### Q11. Base Case Importance (6 marks)
Why is a base case important in recursion?
A) To make the function run faster  
B) To prevent infinite recursion  
C) To use less memory  
D) To make the code more readable

### Q12. Simple Recursion (6 marks)
Write a recursive function that calculates the sum of numbers from 1 to n:
```javascript
function sumToN(n) {
  // Your code here
}
// sumToN(5) should return 15 (1+2+3+4+5)
```

---

## SECTION E: SORTING CONCEPTS (DAY 7) (20 marks)

### Q13. Sorting Properties (8 marks)
Which statement about sorting algorithms is TRUE?
A) Bubble sort is efficient for large datasets  
B) Merge sort has O(n²) time complexity  
C) Built-in sort methods in JS/Python are stable  
D) Quick sort always performs better than merge sort

### Q14. When to Use Simple Sorts (6 marks)
When might you choose insertion sort over merge sort?
A) When you have a large dataset  
B) When you have a small or nearly sorted dataset  
C) When you need O(n log n) guaranteed performance  
D) When you need to sort objects by multiple fields

### Q15. Sorting Implementation (6 marks)
Complete this bubble sort implementation:
```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // Swap elements
        const temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

---

## SCORING GUIDE

| Score | Level | Action |
|-------|-------|--------|
| 90-100 | Excellent | Ready for advanced topics |
| 80-89 | Good | Minor gaps to review |
| 70-79 | Satisfactory | Needs review of weaker areas |
| Below 70 | Significant gaps | Consider reviewing days 3-7 |

**Instructions:**
1. Complete all sections without assistance
2. For coding questions, write your answer in JavaScript or Python
3. For explanation questions, be concise but complete
4. Check your work if time permits

---
*When you complete this assessment, check your answers against the key to see what you've mastered and what needs review.*