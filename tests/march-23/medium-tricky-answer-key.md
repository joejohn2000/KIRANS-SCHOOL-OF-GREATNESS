# MEDIUM TRICKY FOCUS ASSESSMENT - ANSWER KEY

## SECTION A: APPEARANCE VS REALITY

### Q1. The Deceptive Loop
**Answer: B) 3, 3, 3 (after 100ms)**  
Explanation: This is the classic closure-in-loop problem with `var`. The `setTimeout` callbacks are executed after the loop completes, by which time `i` has reached 3. All three callbacks reference the same `i` variable (function-scoped due to `var`), so they all print 3. The loop itself completes immediately (no output), and the callbacks execute after 100ms.

### Q2. The Array That Lies
**Answer: C) 11**  
Explanation: In JavaScript, arrays are sparse when you assign to an index beyond the current length. Setting `arr[10] = 99` on an array of length 5 creates a new array with length 11, where indices 6-9 are empty (undefined). The length property reflects the highest index + 1.

### Q3. The Function That Forgets
**Answer: A) 8 13**  
Explanation: This tests closure understanding. `makeAdder(5)` returns a function that remembers `x = 5` via closure. When called with `y = 3`, it returns 5 + 3 = 8. Similarly, `makeAdder(10)` remembers `x = 10`, so `add10(3)` returns 10 + 3 = 13. Each returned function has its own separate closure scope.

## SECTION B: EDGE CASE MASTERY

### Q4. The Empty Array Trap
**Answer: B) -Infinity**  
Explanation: The spread operator `...arr` on an empty array produces no arguments. `Math.max()` called with no arguments returns `-Infinity`. This is a subtle edge case that many developers overlook.

### Q5. The Off-by-One Illusion
**Answer: C) n = 2**  
Explanation: While the function happens to return the correct value for n=2 (true, since 2 is prime), it does so without entering the loop to check any divisors. For n=2, the loop condition `i < n` (2 < 2) is false immediately, so the loop never executes. This means the function returns true without performing any actual primality testing - it's correct by accident rather than by design. For a proper implementation, we'd want to handle n=2 as a special case or adjust the loop boundary.

### Q6. The String That's Not
**Answer: B) "hello"**  
Explanation: Strings are immutable in JavaScript. Attempting to assign `str[0] = "H"` does not change the string; it fails silently (in non-strict mode) or throws an error in strict mode. The string remains "hello". In strict mode, this would throw a TypeError, but since the question doesn't specify strict mode and the option B exists, we assume non-strict mode where the assignment is ignored.

## SECTION C: IMPLEMENTATION PRECISION

### Q7. The Switch That Slips
**Answer: B) "one" "two" "default"**  
Explanation: This tests understanding of fall-through in switch statements. Without `break` statements, execution continues to the next case. For `x = 1`: matches case 1, logs "one", then continues to case 2 (logs "two"), then default (logs "default").

### Q8. The Parameters That Shift
**Answer: A) 5 1**  
Explanation: This tests default parameters. When `test(5)` is called, `a` receives the value 5. No second argument is provided, so parameter `b` gets its default value of 1. The function logs "5 1".

### Q9. The Return That Forgets
**Answer: A) [2,4,6]**  
Explanation: The `forEach` method iterates over the array and doubles each element in place (`arr[idx] = val * 2`). After the loop, `arr` is modified to `[2,4,6]` and this same array is returned. The function does not create a new array; it modifies the original and returns it.

## SECTION D: PATTERN RECOGNITION UNDER PRESSURE

### Q10. The Nested Scope Switch
**Answer: A) inner outer global**  
Explanation: This tests lexical scoping nesting. 
- `inner()`: looks for `x` in its scope (finds "inner"), logs "inner"
- After `inner()` returns, `outer()` logs its `x` ("outer") 
- Finally, the global scope logs its `x` ("global")
Each function looks outward through its lexical scope chain to find variable bindings.

### Q11. The Async Microtask Maze
**Answer: start, end, microtask1, promise1, promise2, timeout1, timeout2**  
Explanation: 
1. Synchronous: 'start' → 'end' 
2. Microtasks (highest priority): queued in order - 'microtask1', then first 'promise1' (from first .then()), then 'promise2' (from second .then() inside the first .then())
3. Macrotasks (setTimeout): 'timeout1' then 'timeout2' (from inside the second .then())
Note: The second .then() creates a promise that logs 'promise2' THEN queues 'timeout2', so 'promise2' comes before 'timeout2'.

### Q12. The Recursive Window
**Answer: B) 6**  
Explanation: Trace the recursion:
- mystery(4): 4%2===0 → returns 4 + mystery(3)
- mystery(3): 3%2!==0 → returns mystery(2)
- mystery(2): 2%2===0 → returns 2 + mystery(1)
- mystery(1): 1%2!==0 → returns mystery(0)
- mystery(0): n<=0 → returns 0
Now unwind:
- mystery(0) = 0
- mystery(1) = mystery(0) = 0
- mystery(2) = 2 + mystery(1) = 2 + 0 = 2
- mystery(3) = mystery(2) = 2
- mystery(4) = 4 + mystery(3) = 4 + 2 = 6

## SCORING GUIDE
- Questions 1-3: 8 marks each (24 total)
- Questions 4-6: 8 marks each (24 total)  
- Questions 7-9: 8 marks each (24 total)
- Questions 10-12: 8-9 marks each (25 total)
- Total: 100 marks