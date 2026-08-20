# Topic 5: Representation of Algorithm — Pseudocode

## 1. What is Pseudocode?

- **Pseudocode** means "fake code."
- It is a way of writing an algorithm using **simple English-like statements**, structured similarly to real programming code.
- It is **not** written in any specific programming language, so it has no strict syntax rules.
- Its purpose is to describe the **logic** clearly, in a way that can be easily converted into any programming language (C, Java, Python, etc.).

## 2. Why Use Pseudocode?

- Bridges the gap between a plain-English algorithm and actual program code.
- Focuses on **logic**, not on syntax (semicolons, brackets, data types, etc.).
- Easy to convert into real code once the logic is correct.
- Helps programmers plan their program structure before coding.

## 3. Common Pseudocode Conventions

Since pseudocode has no fixed rules, most people follow these common conventions:

| Keyword                        | Meaning                                |
| ------------------------------ | -------------------------------------- |
| `START` / `BEGIN`              | Marks the beginning                    |
| `STOP` / `END`                 | Marks the end                          |
| `INPUT` / `READ`               | Take input from the user               |
| `OUTPUT` / `DISPLAY` / `PRINT` | Show output to the user                |
| `SET` / `=`                    | Assign a value to a variable           |
| `IF ... THEN ... ELSE`         | Decision-making                        |
| `WHILE ... DO`                 | Repeat steps while a condition is true |
| `FOR`                          | Repeat steps a fixed number of times   |

## 4. Difference Between Algorithm and Pseudocode

| Point             | Algorithm                      | Pseudocode                       |
| ----------------- | ------------------------------ | -------------------------------- |
| Language style    | Plain, descriptive sentences   | Structured, code-like statements |
| Closeness to code | Far from actual code           | Very close to actual code        |
| Readability       | Very easy, general description | Slightly more technical          |

## 5. Example 1: Pseudocode to Add Two Numbers

```
START
    READ a, b
    sum = a + b
    DISPLAY sum
STOP
```

## 6. Example 2: Pseudocode to Find the Largest of Three Numbers

```
START
    READ a, b, c
    IF a > b AND a > c THEN
        largest = a
    ELSE IF b > a AND b > c THEN
        largest = b
    ELSE
        largest = c
    ENDIF
    DISPLAY largest
STOP
```

## 7. Example 3: Pseudocode to Check Even or Odd

```
START
    READ n
    remainder = n MOD 2
    IF remainder == 0 THEN
        DISPLAY "Even"
    ELSE
        DISPLAY "Odd"
    ENDIF
STOP
```

*(Note: `MOD` means "modulus," i.e., finding the remainder after division. In C, this is written as `%`.)*

## 8. Example 4: Pseudocode to Find the Factorial of a Number

```
START
    READ n
    fact = 1
    i = 1
    WHILE i <= n DO
        fact = fact * i
        i = i + 1
    ENDWHILE
    DISPLAY fact
STOP
```

## 9. Example 5: Pseudocode to Find the Sum of First N Natural Numbers

```
START
    READ n
    sum = 0
    i = 1
    WHILE i <= n DO
        sum = sum + i
        i = i + 1
    ENDWHILE
    DISPLAY sum
STOP
```

## 10. Advantages of Pseudocode

- Easy to write and modify (no strict syntax rules).
- Focuses purely on logic, not on language-specific details.
- Can be understood by programmers of any language.
- Acts as a bridge between the algorithm and the final source code.

## 11. Limitations of Pseudocode

- No visual representation (unlike flowcharts).
- Since there's no fixed standard, different people may write it differently.
- Cannot be directly executed by a computer (must be converted into real code).

## 12. Quick Recap (One-Line Points)

- Pseudocode = English-like, code-structured way of writing an algorithm.
- No strict syntax rules — focuses on logic only.
- Uses keywords like START, END, READ, DISPLAY, IF-ELSE, WHILE.
- Acts as a bridge between an algorithm and actual source code.
- Very close to real programming code, easy to convert into C, Java, Python, etc.