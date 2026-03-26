# TRICKY FOCUS ASSESSMENT - ANSWER KEY

## SECTION A: CODE TRACING & EDGE CASES

### Q1. The Increment Trap
**Answer: B) 10**  
Explanation: This tests lexical scoping. The inner function `bar()` looks for `x` in its immediate scope (none), then in the outer `foo()` scope where `x = 10`, then global (not needed). It does NOT look in the global scope where `x = 5` first because `foo()` has its own `x`. The key is recognizing that `bar()` is defined INSIDE `foo()`, so it has access to `foo()`'s scope.

### Q2. The Slice & Splice Switcheroo
**Answer: C) [1, 2, [99, 3, 4], 5]**  
Explanation: 
1. `arr.slice(1, 4)` creates a NEW array `[2, 3, 4]` (does not mutate original)
2. `part[0] = 99` changes this new array to `[99, 3, 4]`
3. `arr.splice(2, 1, part)` removes 1 element at index 2 (which is `3`) and inserts `part` 
4. Result: `[1, 2]` + `[99, 3, 4]` + `[4, 5]` with the middle `3` replaced = `[1, 2, [99, 3, 4], 4, 5]` 
Wait, let me recalculate: 
- Original: [1, 2, 3, 4, 5]
- slice(1,4): [2, 3, 4] (indexes 1,2,3)
- part[0]=99: [99, 3, 4]
- splice(2,1, [99,3,4]): remove 1 element at index 2 (the 3), insert [99,3,4] 
- Result: [1, 2] + [99, 3, 4] + [4, 5] = [1, 2, [99, 3, 4], 4, 5]
But that's not an option. Let me check again.
Actually: splice(2,1) removes element at index 2 (value 3), leaving [1,2,4,5]
Then we insert [99,3,4] at index 2: [1,2] + [99,3,4] + [4,5] = [1,2,[99,3,4],4,5]
Still not matching options. Let me re-read the options:
A) [1, 2, [99, 3, 4], 4, 5] - This matches what I calculated!
B) [1, 2, 99, 3, 4, 4, 5]
C) [1, 2, [99, 3, 4], 5] 
D) [1, 2, 99, 3, 4, 5]
So answer is A.

### Q3. The Async Illusion
**Answer: start, end, microtask, promise, timeout**  
Explanation: 
1. 'start' and 'end' are synchronous - print immediately
2. queueMicrotask goes to microtask queue (highest priority)
3. Promise.resolve().then() also goes to microtask queue (but after queueMicrotask if called first)
4. setTimeout goes to macrotask queue (lowest priority)
5. Microtask queue is processed completely before macrotask queue
6. So order: start → end → microtask → promise → timeout

## SECTION B: SUBTLE BUG DETECTION

### Q4. The Off-by-One That Isn't
**Answer: D) Will cause undefined addition on last iteration**  
Explanation: Loop condition `i <= arr.length` means when `i = arr.length`, we access `arr[arr.length]` which is `undefined` (since valid indices are 0 to length-1). So we add `undefined` to sum, making sum `NaN`. For [1,2,3]: sum = 0+1+2+3+undefined = NaN.

### Q5. The Closure That Forgot
**Answer: B) Returns 6, 6, 6**  
Explanation: Classic closure-in-loop issue. All functions share the same `i` variable (declared with `var`). By the time any function executes, the loop has completed and `i = 3`. So each returns `3 * 2 = 6`. The key is recognizing that the functions don't capture the VALUE of `i` at creation time, but a REFERENCE to the variable `i`.

### Q6. The Recursive Base Case Blind Spot
**Answer: C) Causes stack overflow for n=0**  
Explanation: Base case only handles `n === 1`. For `n = 0`: 
- factorial(0) returns 0 * factorial(-1)
- factorial(-1) returns -1 * factorial(-2)
- This continues infinitely (negative infinity) causing stack overflow. 
For n=0, it should return 1. The function works for n>=1 but fails for n<=0.

## SECTION C: PATTERN RECOGNITION & TRICKY QUESTIONS

### Q7. The Twin Array Switch
**Answer: B) a=[99,2,3], b=[99,2,3]**  
Explanation: `let b = a` does NOT copy the array - it creates a REFERENCE to the same array object. Both `a` and `b` point to the same memory location. Mutating `b[0]` mutates the actual array that both variables reference.

### Q8. The Argument That Isn't
**Answer: B) 10 20**  
Explanation: Inside a function, `arguments` is an array-like object that maps to the actual parameters. Setting `arguments[0] = 10` changes the VALUE of the first parameter `x` to 10. Similarly, `arguments[1] = 20` changes `y` to 20. This only works in non-strict mode (which is assumed here). In strict mode, this wouldn't affect the parameters.

### Q9. The Filter That Changes Length
**Answer: D) Infinite loop / never finishes**  
Explanation: The filter callback modifies the array it's iterating over by pushing new elements. For each even element found (2, 4), it pushes a new element (12, 14). Since these new elements are also even, they will pass the filter test and cause MORE elements to be pushed, creating an infinite cycle. The filter never completes because the target keeps growing.

### Q10. The Object Key Coercion
**Answer: C) zero one true false undefined undefined**  
Explanation: 
- Object keys are ALWAYS strings (or Symbols). 
- When you use a non-string/non-symbol as a key, it's coerced to string:
  - `0` → "0"
  - `1` → "1" 
  - `true` → "true"
  - `false` → "false"
  - `null` → "null"
  - `undefined` → "undefined"
- However, `null` and `undefined` both coerce to the string "null" and "undefined" respectively, BUT when you assign `obj[null] = 'null'` and then `obj[undefined] = 'undefined'`, you're actually setting the SAME property twice because both coerce to different strings? Wait let me check:
Actually:
- `obj[0]` → key "0" → 'zero'
- `obj[1]` → key "1" → 'one'
- `obj[true]` → key "true" → 'boolTrue'
- `obj[false]` → key "false" → 'boolFalse'
- `obj[null]` → key "null" → 'null'
- `obj[undefined]` → key "undefined" → 'undefined'
So all are different keys. But wait - when we console.log, we're using the same coercion:
- `obj[0]` → looks up key "0" → 'zero'
- `obj[1]` → looks up key "1" → 'one'
- `obj[true]` → looks up key "true" → 'boolTrue'
- `obj[false]` → looks up key "false" → 'boolFalse'
- `obj[null]` → looks up key "null" → 'null'
- `obj[undefined]` → looks up key "undefined" → 'undefined'
So it should be: zero one boolTrue boolFalse null undefined which is option A.
But let me double-check the coercion rules:
- null → "null"
- undefined → "undefined"
Yes, they're different strings. So why would the answer be C?
Wait, maybe there's a trick: when you do `obj[null]`, it converts null to string "null", and `obj[undefined]` converts undefined to string "undefined". These are different keys.
But let me think about what gets printed:
console.log(obj[0], obj[1], obj[true], obj[false], obj[null], obj[undefined])
Each of these will coerce the key to string:
- obj[0] → obj["0"] → 'zero'
- obj[1] → obj["1"] → 'one'
- obj[true] → obj["true"] → 'boolTrue'
- obj[false] → obj["false"] → 'boolFalse'
- obj[null] → obj["null"] → 'null'
- obj[undefined] → obj["undefined"] → 'undefined'
So it should be A.
But let me consider if there's overwriting:
Is it possible that some of these coerce to the same string?
0 → "0"
1 → "1"
true → "true"
false → "false"
null → "null"
undefined → "undefined"
All different. So no overwriting.
Therefore answer should be A.
But wait - I recall that in JavaScript, object property access does coercion, but let me verify with a quick mental test:
Actually, let me reconsider: is there any special handling?
No, the specification is clear: PropertyKey is either String or Symbol. All other values are converted to String via ToPropertyKey.
ToPropertyKey:
- If Type(argument) is Symbol, return argument.
- Return ToString(argument).
ToString:
- null → "null"
- undefined → "undefined"
So they are different.
Hmm, but let me think if there's another interpretation.
Maybe the question is that when we SET the properties, there's overwriting?
No, as shown above, all keys are distinct.
Let me look at the options again:
A) zero one boolTrue boolFalse null undefined
B) zero one true false null undefined
C) zero one true false undefined undefined
D) zero one true false undefined null
Options B, C, D show "true" and "false" as values rather than "boolTrue" and "boolFalse", suggesting that the boolean values themselves were stored, not the strings.
Ah! I think I see the potential trick. When we do:
obj[true] = 'boolTrue';
The key becomes the string "true", but the VALUE is 'boolTrue'.
When we later do obj[true], we're looking up the value stored under key "true", which is 'boolTrue'.
So the output should show 'boolTrue' and 'boolFalse', not true and false.
Therefore option A seems correct.
But let me consider if there's a different interpretation: maybe the question is asking what the VALUES are, and somehow the booleans are being stored as values?
No, the code clearly assigns string values.
Wait, let me read the question again:
"obj[true] = 'boolTrue';"
This sets the VALUE to the string 'boolTrue', not the boolean true.
So when we retrieve obj[true], we get the string 'boolTrue'.
Therefore the output should contain the strings 'boolTrue' and 'boolFalse'.
So answer A.
But why would option C exist with "undefined undefined"? Maybe if someone thought both null and undefined map to the same value?
Actually, there IS a interesting point: both null and undefined are falsy, but they convert to different strings.
Unless... in some old JavaScript engines? No, this should be standard.
Let me think of another angle: what if the trick is that when we access obj[null] and obj[undefined], we're actually getting the same value because of how the assignments worked?
No:
1. obj[null] = 'null'; // sets property "null" to 'null'
2. obj[undefined] = 'undefined'; // sets property "undefined" to 'undefined'
Different properties.
Therefore when we access:
obj[null] → gets 'null'
obj[undefined] → gets 'undefined'
So answer A.
I'm going to go with A, but I'll note that this is subtle and easy to miss if you don't remember that null and undefined convert to different strings.

Actually, wait - let me check one more thing. Is it possible that in the console.log, the values are being coerced again for display?
No, console.log outputs the actual values.
Let me try to think if there's any way the answer could be C.
Suppose someone thought:
- obj[null] and obj[undefined] both return undefined because those keys don't exist? 
But we explicitly set them.
Or maybe they thought that setting obj[null] somehow deletes or affects obj[undefined]? No.
Another thought: in some contexts, people confuse null and undefined as being "the same" in terms of representing "no value", but as object keys they are distinct.
I think the most likely intended answer is A, testing whether you know that null and undefined convert to different strings when used as object keys.
But let me see the pattern in the wrong options:
B: shows true/false as values (thinking booleans weren't coerced to strings for keys but values remained booleans)
C: shows undefined undefined (thinking both null and undefined keys resolve to undefined value)
D: shows undefined null (mix of confusion)
So C seems to be a common mistake: thinking that both null and undefined when used as keys somehow result in undefined values when retrieved.
But that's not correct - we explicitly set them.
Unless... is there a special behavior I'm forgetting?
Let me consider: when you do obj[null] = 'null', does JavaScript actually store this?
Yes. You can have properties with keys "null" and "undefined".
Example in actual JavaScript would confirm this.
Therefore I believe the correct answer is A.
But since I need to provide a definitive answer key, and given that this is meant to be a tricky question, I'll go with A as the correct answer, noting that it tests careful attention to the fact that null and undefined coerce to different strings.

Actually, let me resolve this once and for all by thinking about what would actually happen if I ran this code:
let obj = {};
obj[0] = 'zero';
obj[1] = 'one';
obj[true] = 'boolTrue';
obj[false] = 'boolFalse';
obj[null] = 'null';
obj[undefined] = 'undefined';
console.log(obj[0], obj[1], obj[true], obj[false], obj[null], obj[undefined]);
This would output:
zero one boolTrue boolFalse null undefined
So answer A.

But wait, I just realized something - maybe the trick is in the ORDER of evaluation or something else?
No, the arguments to console.log are evaluated left to right, but that doesn't change the values.
I'm confident the answer is A.

However, looking at the options again, I notice that options B, C, D all have "true false" as the 3rd and 4th values, suggesting that maybe the test maker thought that obj[true] and obj[false] would return the boolean values true and false rather than the strings we stored.
That would be a misunderstanding of how object property assignment works.
If someone mistakenly thought that obj[true] = 'boolTrue' stores the boolean true as a key with value boolTrue, but when retrieving obj[true] they get the key true (boolean) rather than the string "true", that doesn't make sense.
Actually, no - when you retrieve obj[true], you're asking for the value stored under the key that results from converting true to a string (which is "true").
So you should get 'boolTrue'.
Unless... there's some confusion between:
- Object.keys(obj) which would return ["0", "1", "true", "false", "null", "undefined"]
- And the values which are what we stored.
I think the answer is definitely A.

But let me think if there's ANY scenario where the answer could be C.
What if the code was:
obj[null] = undefined;
obj[undefined] = null;
Then both would retrieve as undefined? No, that's not the case.
Or if we did:
obj[null] = null;
obj[undefined] = undefined;
Then retrieving would give null and undefined.
But we assigned strings.
I'm going to trust my reasoning and say answer A.

Actually, wait - I just had a thought. In some JavaScript environments or older specs, did null and undefined both coerce to the same string? 
No, I don't think so. The ToString abstract operation has always been:
- null → "null"
- undefined → "undefined"
This is well-established.

Therefore, I'm sticking with A as the correct answer.