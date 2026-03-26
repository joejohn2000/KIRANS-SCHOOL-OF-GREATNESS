# ANSWER SHEET — MEDIUM TRICKY FOCUS ASSESSMENT
**Date:** March 23, 2026
**Total Marks:** 100

---

## SECTION A: APPEARANCE VS REALITY (25 marks)

### Q1. The Deceptive Loop — **Answer: B** (8 marks)
> 3, 3, 3 (after 100ms)

`var` is function-scoped, not block-scoped. All three arrow functions share the **same** `i` variable. By the time the 100ms timeouts fire, the loop has already finished and `i` has been incremented to `3`. All three callbacks print `3`.

Fix: use `let` instead of `var`, or wrap in an IIFE to capture `i` per iteration.

---

### Q2. The Array That Lies — **Answer: C** (8 marks)
> 11

Setting `arr[10] = 99` creates a **sparse array**. JavaScript sets `length` to the highest index + 1. Indices 5–9 exist as "holes" (not undefined, but empty). `arr.length` → `11`.

---

### Q3. The Function That Forgets — **Answer: A** (9 marks)
> 8 13

`makeAdder` returns a closure that captures its own copy of `x`. Each call to `makeAdder` creates a fresh closure with a distinct `x`:
- `add5(3)` → `5 + 3 = 8`
- `add10(3)` → `10 + 3 = 13`

---

## SECTION B: EDGE CASE MASTERY (25 marks)

### Q4. The Empty Array Trap — **Answer: B** (8 marks)
> -Infinity

Spreading `[]` passes **zero arguments** to `Math.max()`. By ECMAScript specification, `Math.max()` with no arguments returns `-Infinity`. This is the identity element for the max operation.

---

### Q5. The Off-by-One Illusion — **Answer: C** (8 marks)
> n = 1.5

The loop condition is `i < n`. For `n = 1.5`, the loop starts at `i = 2`, but `2 < 1.5` is **false** — the loop body never executes. The function falls through to `return true`, incorrectly identifying `1.5` as prime.

The other options all return correctly:
- `n = 0` → returns `false` ✓ (caught by `n < 2`)
- `n = 1` → returns `false` ✓ (caught by `n < 2`)
- `n = 4` → returns `false` ✓ (`4 % 2 === 0` triggers on `i = 2`)

---

### Q6. The String That's Not — **Answer: B** (9 marks)
> "hello"

Strings are **immutable** in JavaScript. The assignment `str[0] = "H"` silently does nothing in non-strict mode — no error is thrown, but `str` remains `"hello"`. To modify a string, you must create a new one (e.g., `"H" + str.slice(1)`).

---

## SECTION C: IMPLEMENTATION PRECISION (25 marks)

### Q7. The Switch That Slips — **Answer: B** (8 marks)
> "one" "two" "default"

There are **no `break` statements**. Once `case 1:` matches, execution falls through every subsequent case — `case 2:` and `default:` — printing all three values.

Fix: add `break;` after each case block.

---

### Q8. The Parameters That Shift — **Answer: A** (8 marks)
> 5 1

Default parameters activate when the argument is **`undefined`** (not just falsy). Since `b` is not passed, it receives its default value of `1`. Output: `5 1`.

---

### Q9. The Return That Forgets — **Answer: A** (9 marks)
> [2,4,6]

`forEach` iterates and **mutates the original array in place** via `arr[idx] = val * 2`. The function then returns the same array reference. Output: `[2, 4, 6]`.

Watch out: this also mutates the caller's original array — a common unintended side effect.

---

## SECTION D: PATTERN RECOGNITION UNDER PRESSURE (25 marks)

### Q10. The Nested Scope Switch — **Answer: A** (8 marks)
> inner outer global

Each `let x` declaration creates an **independent binding** in its own block scope. The three `console.log(x)` calls each resolve to the nearest enclosing scope:
1. Inside `inner()` → `"inner"`
2. Inside `outer()`, after `inner()` returns → `"outer"`
3. Global scope → `"global"`

---

### Q11. The Async Microtask Maze — **Answer:** (9 marks)

```
start
end
promise1
microtask1
promise2
timeout1
timeout2
```

**Execution order explained:**

| Phase | What runs | Why |
|---|---|---|
| Synchronous | `start`, `end` | Runs immediately, top to bottom |
| Microtask queue | `promise1`, `microtask1`, `promise2` | Microtasks drain completely before any macrotask. Both `Promise.resolve().then()` and `queueMicrotask()` are microtasks, processed in registration order |
| `promise2` schedules `timeout2` | — | This `setTimeout` is queued during the microtask phase |
| Macrotask queue | `timeout1`, then `timeout2` | `timeout1` was queued before `timeout2`, so it runs first |

Key rule: **Microtask queue always fully drains before the next macrotask executes.**

---

### Q12. The Recursive Window — **Answer: B** (8 marks)
> 6

Full trace:

| Call | n even/odd | Result |
|---|---|---|
| `mystery(4)` | even | `4 + mystery(3)` |
| `mystery(3)` | odd | `mystery(2)` |
| `mystery(2)` | even | `2 + mystery(1)` |
| `mystery(1)` | odd | `mystery(0)` |
| `mystery(0)` | base case | `0` |

Resolving bottom-up:
- `mystery(1)` = `0`
- `mystery(2)` = `2 + 0` = `2`
- `mystery(3)` = `2`
- `mystery(4)` = `4 + 2` = **6**

The function sums only **even** numbers ≤ n.

---

## MARK SUMMARY

| Q | Answer | Marks |
|---|---|---|
| Q1 | B | 8 |
| Q2 | C | 8 |
| Q3 | A | 9 |
| Q4 | B | 8 |
| Q5 | C | 8 |
| Q6 | B | 9 |
| Q7 | B | 8 |
| Q8 | A | 8 |
| Q9 | A | 9 |
| Q10 | A | 8 |
| Q11 | (see sequence above) | 9 |
| Q12 | B | 8 |
| **Total** | | **100** |
