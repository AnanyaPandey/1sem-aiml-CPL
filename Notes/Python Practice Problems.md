# Python Practice Problems

No solutions included on purpose — work through each one yourself. Ask if you get stuck or want your solution reviewed.

Ordered roughly easy → hard. Topics 6–10 come up a LOT in LangChain/LangGraph-style agentic code, so don't skip those even if OOP feels rusty.

------

## 1. *args / **kwargs — Order-independent formatter

Write a function `build_profile(name, *hobbies, **details)` that:

- Takes a required `name`
- Takes any number of hobbies (positional)
- Takes any number of extra details (keyword) like `age`, `city`, etc.
- Returns a single formatted string like: `"Ananya likes chess, running. Details: age=35, city=Jagdalpur"`

**Hint:** you'll need to join a tuple and format a dict's items.

------

## 2. Closures — Counter factory

Write a function `make_counter(start=0)` that returns another function. Each time the returned function is called, it should increase an internal counter by 1 and return the new value — without using any global variable.

```python
counter = make_counter()
counter()  # 1
counter()  # 2
counter2 = make_counter(100)
counter2()  # 101
counter()  # 3   (independent from counter2)
```

**Hint:** look up the `nonlocal` keyword.

------

## 3. Decorators — Timing and logging

Write a decorator `@log_call` that, when applied to any function, prints:

- the function name and arguments it was called with
- the return value
- how long it took to run

```python
@log_call
def add(a, b):
    return a + b

add(2, 3)
# Output something like:
# Calling add(2, 3)
# add returned 5 in 0.0001s
```

**Hint:** decorators are just functions that take a function and return a wrapped version. Use `*args, **kwargs` here — this is exactly why you learned them.

------

## 4. Generators — Lazy Fibonacci

Write a generator function `fib_gen(limit)` that yields Fibonacci numbers one at a time, up to `limit` count — without storing the whole sequence in a list.

```python
list(fib_gen(7))  # [0, 1, 1, 2, 3, 5, 8]
```

Then explain to yourself (in a comment) why this uses less memory than building a list of a million Fibonacci numbers.

------

## 5. Exception handling — Custom exceptions + retry logic

- Create a custom exception class `InvalidAgeError(Exception)`.
- Write a function `set_age(age)` that raises `InvalidAgeError` if age is negative or above 120.
- Write a wrapper function `safe_set_age(age, retries=3)` that calls `set_age`, and if it fails, asks for a new age (simulate with a hardcoded list of fallback values) up to `retries` times before giving up and printing a final failure message.

**Why this matters:** retry logic like this is everywhere in agentic AI code (an LLM call fails or returns bad output → retry).

------

## 6. OOP — Class + inheritance with a twist

Build a small class hierarchy:

- `Shape` (base class) with a method `area()` that raises `NotImplementedError`
- `Rectangle` and `Circle` that inherit from `Shape` and implement `area()`
- Add a class method `Shape.total_area(shapes: list)` that takes a list of shape objects (mixed types) and returns the sum of all their areas

```python
shapes = [Rectangle(3, 4), Circle(5), Rectangle(2, 2)]
Shape.total_area(shapes)
```

**Hint:** this is testing polymorphism — the same method name behaving differently per class.

------

## 7. Dictionaries as dispatch tables — Mini calculator

Instead of writing a big if/elif chain, build a calculator using a dictionary that maps operator strings to functions:

```python
def calculate(a, b, op):
    operations = {
        "+": lambda x, y: x + y,
        "-": lambda x, y: x - y,
        # add *, /, and handle divide-by-zero
    }
    ...
```

Handle an unknown operator by raising a clear error, and handle division by zero without crashing ugly.

**Why this matters:** this "dictionary of functions" pattern is exactly how tool-routing works in agent frameworks (mapping a tool name to the function that executes it).

------

## 8. Context managers — Custom `with` block

Without using `contextlib`, write a class `Timer` that can be used like this:

```python
with Timer("data load"):
    time.sleep(1)   # simulate work
# Output: "data load took 1.00 seconds"
```

**Hint:** you need to implement `__enter__` and `__exit__` methods.

------

## 9. Recursion + memoization

Write a recursive function `count_paths(m, n)` that counts the number of unique paths from the top-left to bottom-right of an `m x n` grid, moving only right or down.

Then add memoization (a dictionary cache, or `functools.lru_cache`) and print how many recursive calls happen with vs. without memoization for a 15x15 grid.

**Hint:** `count_paths(m, n) = count_paths(m-1, n) + count_paths(m, n-1)`, with base cases when m or n is 1.

------

## 10. Put it together — Mini agent-style task router

This one combines several of the above. Build a tiny "agent" that:

1. Has a dictionary of available "tools" (functions) — e.g. `add`, `multiply`, `get_weather` (fake it — just return a hardcoded string), `to_uppercase`
2. Has a function `run_agent(task_name, *args, **kwargs)` that:
   - Looks up the tool by name in the dictionary
   - If not found, raises a clear custom exception (`ToolNotFoundError`)
   - Calls the tool with whatever args/kwargs were passed
   - Logs the call using your `@log_call` decorator from Problem 3
   - Catches any error the tool raises and returns a friendly failure message instead of crashing

```python
run_agent("add", 4, 5)              # 9
run_agent("get_weather", city="Durg")  # fake weather string
run_agent("nonexistent_tool")       # friendly error, not a crash
```

**Why this matters:** this is a simplified but real shape of how LangChain/LangGraph tool-calling works under the hood — a registry of tools, a dispatcher, and error handling around each call. Once this feels natural, the "tool calling" concept in your Udemy course will click much faster.

------

## How to use this

- Do them in order — 6 through 10 lean on ideas from 1 through 5
- Don't look up solutions right away if you get stuck — try for 15-20 minutes first, then ask me for a hint (not the full answer)
- Once done, paste me your code for any of these and I'll review it and point out rough edges