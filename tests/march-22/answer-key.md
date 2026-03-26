# DAY 22 ASSESSMENT | DAYS 1-7 REVIEW - ANSWER KEY

## SECTION A: BIG O COMPLEXITY (DAY 3)

### Q1. Time Complexity Analysis
**Answer: B) O(n)**  
Explanation: The function iterates through the array once, comparing each element to the current maximum. This results in n-1 comparisons, which is O(n).

### Q2. Space Complexity
**Answer: A) O(1)**  
Explanation: The function uses a constant amount of extra space (variables `max` and `i`), regardless of input size.

### Q3. Nested Loops
**Answer: C) O(n²)**  
Explanation: For each element in the array, the inner loop checks all subsequent elements. This results in approximately n²/2 comparisons, which simplifies to O(n²).

## SECTION B: ARRAY/LIST OPERATIONS (DAY 4)

### Q4. Array Methods
**Answer: B) 24**  
Explanation: 
1. `map`: [1,2,3,4,5] → [2,4,6,8,10] 
2. `filter`: [2,4,6,8,10] → [2,4,6,8,10] (all are even)
3. `reduce`: 2+4+6+8+10 = 30

Wait, let me recalculate: 2+4+6+8+10 = 30, not 24. Let me check again.

Actually: 
1. `map`: [1,2,3,4,5] → [2,4,6,8,10] 
2. `filter`: [2,4,6,8,10] → [2,4,6,8,10] (all elements are even)
3. `reduce`: 2+4+6+8+10 = 30

So the answer should be C) 30.

### Q5. Two-Pointer Technique
**Answer: B) Finding two numbers in a sorted array that add up to a target**  
Explanation: The two-pointer technique is ideal for sorted arrays when you need to find pairs that meet a condition (like summing to a target). You start with pointers at both ends and move them inward based on whether the current sum is too high or too low.

### Q6. Array Transformation
**Answer:**
```javascript
function squareArray(arr) {
  return arr.map(x => x * x);
}
// or
function squareArray(arr) {
  const result = [];
  for (let i = 0; i < arr.length; i++) {
    result.push(arr[i] * arr[i]);
  }
  return result;
}
```

## SECTION C: DICTIONARIES/HASH MAPS (DAY 5)

### Q7. Hash Map Usage
**Answer: C) 3**  
Explanation: The letter 'a' appears 3 times in the array ['a', 'b', 'a', 'c', 'b', 'a'].

### Q8. When to Use Hash Maps
**Answer: B) When you need fast lookups by key**  
Explanation: Hash maps provide O(1) average time complexity for lookups, insertions, and deletions, making them ideal when you need to quickly access values by their keys.

### Q9. Frequency Counter
**Answer:**
```javascript
function mostFrequent(arr) {
  const counts = {};
  let maxCount = 0;
  let mostFrequentElement = null;
  
  for (const element of arr) {
    counts[element] = (counts[element] || 0) + 1;
    if (counts[element] > maxCount) {
      maxCount = counts[element];
      mostFrequentElement = element;
    }
  }
  
  return mostFrequentElement;
}
// Alternative using Object.entries:
function mostFrequent(arr) {
  const counts = {};
  for (const element of arr) {
    counts[element] = (counts[element] || 0) + 1;
  }
  return Object.entries(counts).reduce((a, b) => counts[a[0]] > counts[b[0]] ? a : b)[0];
}
```

## SECTION D: RECURSION (DAY 6)

### Q10. Recursive Factorial
**Answer: D) 24**  
Explanation: factorial(4) = 4 × factorial(3) = 4 × 3 × factorial(2) = 4 × 3 × 2 × factorial(1) = 4 × 3 × 2 × 1 × factorial(0) = 4 × 3 × 2 × 1 × 1 = 24

### Q11. Base Case Importance
**Answer: B) To prevent infinite recursion**  
Explanation: Without a base case, the recursive function would continue calling itself indefinitely until the call stack overflows.

### Q12. Simple Recursion
**Answer:**
```javascript
function sumToN(n) {
  if (n <= 0) {
    return 0;
  }
  return n + sumToN(n - 1);
}
// or
function sumToN(n) {
  return n === 0 ? 0 : n + sumToN(n - 1);
}
```

## SECTION E: SORTING CONCEPTS (DAY 7)

### Q13. Sorting Properties
**Answer: C) Built-in sort methods in JS/Python are stable**  
Explanation: JavaScript's Array.prototype.sort() and Python's sorted()/list.sort() are stable sorting algorithms (Timsort in Python, and modern engines use stable sorts for JS).

### Q14. When to Use Simple Sorts
**Answer: B) When you have a small or nearly sorted dataset**  
Explanation: Insertion sort performs well on small datasets (O(n²) but with low constant factors) and nearly sorted data (can approach O(n)).

### Q15. Sorting Implementation
**Answer:** The implementation provided in the question is already correct. The swap code is properly implemented:
```javascript
if (arr[j] > arr[j + 1]) {
  // Swap elements
  const temp = arr[j];
  arr[j] = arr[j + 1];
  arr[j + 1] = temp;
}
```

## SCORING

Each question is worth the points indicated in the assessment:
- Section A: 3 questions = 20 points (8+6+6)
- Section B: 3 questions = 20 points (8+6+6)
- Section C: 3 questions = 20 points (8+6+6)
- Section D: 3 questions = 20 points (8+6+6)
- Section E: 3 questions = 20 points (8+6+6)
- Total: 100 points

To calculate the score, award points for each correct answer according to the marking scheme in the original assessment.