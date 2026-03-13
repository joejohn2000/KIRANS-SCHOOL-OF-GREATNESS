# DAILY ASSESSMENT 13 MAR | KIRAN’S SCHOOL OF GREATNESS

**Total Marks: 100**  
**Time Allowed: 60 minutes**  
**Instructions:** Answer all questions. Show work where applicable.

---

## SECTION A: Multiple Choice (20 marks - 2 marks each)

### JavaScript Concepts
1. What will this code output?
```javascript
console.log(typeof null);
```
A) "object"  
B) "null"  
C) "undefined"  
D) "boolean"

2. Which statement about `var`, `let`, and `const` is TRUE?
A) `var` is block-scoped  
B) `let` can be redeclared in the same scope  
C) `const` prevents reassignment but not mutation of objects/arrays  
D) All are function-scoped

3. What will this code output?
```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
```
A) 0, 1, 2  
B) 1, 2, 3  
C) 3, 3, 3  
D) 0, 0, 0

### Python Concepts
4. What will this code output?
```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)
```
A) [1, 2, 3]  
B) [1, 2, 3, 4]  
C) [1, 2, 4]  
D) Error

5. Which statement about Python variables is TRUE?
A) Integers are mutable  
B) Strings are mutable  
C) Assignment creates a copy of the object  
D) Variables are references to objects

6. What will this code output?
```python
def modify_list(lst):
    lst.append(4)
    lst = [1, 2, 3]

numbers = [5, 6]
modify_list(numbers)
print(numbers)
```
A) [5, 6]  
B) [5, 6, 4]  
C) [1, 2, 3]  
D) [1, 2, 3, 4]

### Control Flow & Functions
7. In JavaScript, what is the output?
```javascript
function foo() {
  let x = 1;
  if (true) {
    let x = 2;
    console.log(x);
  }
  console.log(x);
}
foo();
```
A) 1, 1  
B) 2, 2  
C) 2, 1  
D) 1, 2

8. Which loop will execute at least once?
A) `while (false) { ... }`  
B) `for (let i = 0; i < 0; i++) { ... }`  
C) `do { ... } while (false);`  
D) All of the above

9. What is the correct way to define an arrow function that returns an object?
A) `() => { return {a: 1}; }`  
B) `() => {a: 1}`  
C) `() => ({a: 1})`  
D) Both A and C

10. In Python, what does `nonlocal` allow you to do?
A) Access global variables  
B) Modify variables in the nearest enclosing scope (not global)  
C) Create new local variables  
D) Access built-in functions

---

## SECTION B: Short Answer (30 marks - 5 marks each)

11. Explain the difference between `==` and `===` in JavaScript. Give one example where they differ. (5 marks)

12. What is a closure in JavaScript? Explain why the following code prints 3 three times instead of 0, 1, 2:  
```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```  
How would you fix it using `let`? (5 marks)

13. Explain the difference between mutable and immutable objects in Python. Give one example of each and show how mutation behaves differently. (5 marks)

14. Write a Python function that uses `nonlocal` to create a counter with `increment()` and `get_value()` methods. (5 marks)

15. Explain the difference between function declaration and function expression in JavaScript. When would you prefer one over the other? (5 marks)

---

## SECTION C: Coding Prediction (30 marks - 6 marks each)

16. What will this JavaScript code output? Explain your reasoning.  
```javascript
var x = 1;
function outer() {
  var x = 2;
  function inner() {
    console.log(x);
  }
  return inner;
}
var func = outer();
func();
```  
(6 marks)

17. What will this Python code output? Explain your reasoning.  
```python
def make_counter():
    count = 0
    def increment():
        nonlocal count
        count += 1
        return count
    return increment

counter1 = make_counter()
counter2 = make_counter()
print(counter1())
print(counter1())
print(counter2())
```  
(6 marks)

18. Predict the output of this JavaScript code and explain why:  
```javascript
console.log(0 == false);
console.log(1 == true);
console.log(2 == true);
console.log(false == false);
console.log(null == undefined);
console.log(null === undefined);
```  
(6 marks)

19. What will this Python code output? Explain your reasoning.  
```python
a = [[1, 2], [3, 4]]
b = a.copy()
b[0][0] = 99
print(a)
print(b)
```  
(6 marks)

20. Write the output of this JavaScript code and explain the scope behavior:  
```javascript
function test() {
  console.log(a);
  console.log(b);
  
  var a = 1;
  let b = 2;
}
test();
```  
(6 marks)

---

## SECTION D: Practical Application (20 marks)

21. **JavaScript Coding Challenge (10 marks)**  
Write a function `createCounter()` that returns an object with three methods:  
- `increment()` - increases the internal count by 1  
- `decrement()` - decreases the internal count by 1  
- `getCount()` - returns the current count  

The count must be private (not accessible directly from the returned object) and persistent between method calls. Use a closure to achieve this.

22. **Python Coding Challenge (10 marks)**  
Write a function `fibonacci_memoized(n)` that returns the nth Fibonacci number using memoization (caching) to optimize performance. The function should:  
- Handle n = 0 and n = 1 as base cases  
- Use a dictionary to cache previously computed results  
- Return the Fibonacci number for any non-negative integer n  

Do NOT use any external libraries or built-in memoization decorators.

---

## SCORING GUIDE
- **90-100**: Excellent mastery - Ready to advance  
- **80-89**: Good understanding - Minor gaps to review  
- **70-79**: Satisfactory - Needs review of weaker areas  
- **Below 70**: Significant gaps - Consider repeating days 1-2  

**Instructions for Student:**  
1. Complete all sections without assistance  
2. For coding questions, write your answer in the language specified  
3. For explanation questions, be concise but complete  
4. Check your work if time permits  

**Instructions for Evaluator:**  
- Award partial credit for partially correct answers  
- For coding questions: correctness (60%), clarity/explanation (40%)  
- For explanation questions: accuracy (70%), completeness (30%)  
- Look for understanding of core concepts, not just memorization  

---  
**END OF ASSESSMENT**  
*When the student completes this assessment, return their answers for evaluation and further plan adjustment.*# 30-Day Plan Assessment: Days 1-2
## JavaScript & Python Fundamentals
**Total Marks: 100**  
**Time Allowed: 60 minutes**  
**Instructions:** Answer all questions. Show work where applicable.

---

## SECTION A: Multiple Choice (20 marks - 2 marks each)

### JavaScript Concepts
1. What will this code output?
```javascript
console.log(typeof null);
```
A) "object"  
B) "null"  
C) "undefined"  
D) "boolean"

2. Which statement about `var`, `let`, and `const` is TRUE?
A) `var` is block-scoped  
B) `let` can be redeclared in the same scope  
C) `const` prevents reassignment but not mutation of objects/arrays  
D) All are function-scoped

3. What will this code output?
```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
```
A) 0, 1, 2  
B) 1, 2, 3  
C) 3, 3, 3  
D) 0, 0, 0

### Python Concepts
4. What will this code output?
```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)
```
A) [1, 2, 3]  
B) [1, 2, 3, 4]  
C) [1, 2, 4]  
D) Error

5. Which statement about Python variables is TRUE?
A) Integers are mutable  
B) Strings are mutable  
C) Assignment creates a copy of the object  
D) Variables are references to objects

6. What will this code output?
```python
def modify_list(lst):
    lst.append(4)
    lst = [1, 2, 3]

numbers = [5, 6]
modify_list(numbers)
print(numbers)
```
A) [5, 6]  
B) [5, 6, 4]  
C) [1, 2, 3]  
D) [1, 2, 3, 4]

### Control Flow & Functions
7. In JavaScript, what is the output?
```javascript
function foo() {
  let x = 1;
  if (true) {
    let x = 2;
    console.log(x);
  }
  console.log(x);
}
foo();
```
A) 1, 1  
B) 2, 2  
C) 2, 1  
D) 1, 2

8. Which loop will execute at least once?
A) `while (false) { ... }`  
B) `for (let i = 0; i < 0; i++) { ... }`  
C) `do { ... } while (false);`  
D) All of the above

9. What is the correct way to define an arrow function that returns an object?
A) `() => { return {a: 1}; }`  
B) `() => {a: 1}`  
C) `() => ({a: 1})`  
D) Both A and C

10. In Python, what does `nonlocal` allow you to do?
A) Access global variables  
B) Modify variables in the nearest enclosing scope (not global)  
C) Create new local variables  
D) Access built-in functions

---

## SECTION B: Short Answer (30 marks - 5 marks each)

11. Explain the difference between `==` and `===` in JavaScript. Give one example where they differ. (5 marks)

12. What is a closure in JavaScript? Explain why the following code prints 3 three times instead of 0, 1, 2:  
```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```  
How would you fix it using `let`? (5 marks)

13. Explain the difference between mutable and immutable objects in Python. Give one example of each and show how mutation behaves differently. (5 marks)

14. Write a Python function that uses `nonlocal` to create a counter with `increment()` and `get_value()` methods. (5 marks)

15. Explain the difference between function declaration and function expression in JavaScript. When would you prefer one over the other? (5 marks)

---

## SECTION C: Coding Prediction (30 marks - 6 marks each)

16. What will this JavaScript code output? Explain your reasoning.  
```javascript
var x = 1;
function outer() {
  var x = 2;
  function inner() {
    console.log(x);
  }
  return inner;
}
var func = outer();
func();
```  
(6 marks)

17. What will this Python code output? Explain your reasoning.  
```python
def make_counter():
    count = 0
    def increment():
        nonlocal count
        count += 1
        return count
    return increment

counter1 = make_counter()
counter2 = make_counter()
print(counter1())
print(counter1())
print(counter2())
```  
(6 marks)

18. Predict the output of this JavaScript code and explain why:  
```javascript
console.log(0 == false);
console.log(1 == true);
console.log(2 == true);
console.log(false == false);
console.log(null == undefined);
console.log(null === undefined);
```  
(6 marks)

19. What will this Python code output? Explain your reasoning.  
```python
a = [[1, 2], [3, 4]]
b = a.copy()
b[0][0] = 99
print(a)
print(b)
```  
(6 marks)

20. Write the output of this JavaScript code and explain the scope behavior:  
```javascript
function test() {
  console.log(a);
  console.log(b);
  
  var a = 1;
  let b = 2;
}
test();
```  
(6 marks)

---

## SECTION D: Practical Application (20 marks)

21. **JavaScript Coding Challenge (10 marks)**  
Write a function `createCounter()` that returns an object with three methods:  
- `increment()` - increases the internal count by 1  
- `decrement()` - decreases the internal count by 1  
- `getCount()` - returns the current count  

The count must be private (not accessible directly from the returned object) and persistent between method calls. Use a closure to achieve this.

22. **Python Coding Challenge (10 marks)**  
Write a function `fibonacci_memoized(n)` that returns the nth Fibonacci number using memoization (caching) to optimize performance. The function should:  
- Handle n = 0 and n = 1 as base cases  
- Use a dictionary to cache previously computed results  
- Return the Fibonacci number for any non-negative integer n  

Do NOT use any external libraries or built-in memoization decorators.

---

## SCORING GUIDE
- **90-100**: Excellent mastery - Ready to advance  
- **80-89**: Good understanding - Minor gaps to review  
- **70-79**: Satisfactory - Needs review of weaker areas  
- **Below 70**: Significant gaps - Consider repeating days 1-2  

**Instructions for Student:**  
1. Complete all sections without assistance  
2. For coding questions, write your answer in the language specified  
3. For explanation questions, be concise but complete  
4. Check your work if time permits  

**Instructions for Evaluator:**  
- Award partial credit for partially correct answers  
- For coding questions: correctness (60%), clarity/explanation (40%)  
- For explanation questions: accuracy (70%), completeness (30%)  
- Look for understanding of core concepts, not just memorization  

---  
**END OF ASSESSMENT**  
*When the student completes this assessment, return their answers for evaluation and further plan adjustment.*
