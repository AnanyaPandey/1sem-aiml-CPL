# Topic 3: Idea of Algorithm

## 1. What is an Algorithm?

- An **algorithm** is a **step-by-step set of instructions** to solve a problem.
- It is like a recipe: a fixed sequence of steps that, if followed correctly, gives the correct result every time.
- An algorithm is written in **plain language** (not in any programming language), so anyone can understand it.

### Simple Example (Everyday Life)

Algorithm to make a cup of tea:

1. Boil water.
2. Add tea leaves.
3. Add milk and sugar.
4. Boil for 2 minutes.
5. Strain into a cup.
6. Serve.

This is exactly how we think about algorithms in programming — a clear sequence of steps.

## 2. Why Do We Need Algorithms?

- Before writing any program, we must first plan **how** to solve the problem.
- An algorithm helps us think through the logic clearly, without worrying about programming language syntax.
- It reduces mistakes because the logic is planned first, then converted into code.

## 3. Characteristics of a Good Algorithm

| Characteristic    | Meaning                                                      |
| ----------------- | ------------------------------------------------------------ |
| **Input**         | It should take zero or more inputs                           |
| **Output**        | It should produce at least one output                        |
| **Definiteness**  | Each step must be clear and unambiguous (no confusion)       |
| **Finiteness**    | It must end after a limited number of steps (should not run forever) |
| **Effectiveness** | Each step must be simple enough to be carried out easily     |

## 4. Steps to Solve Logical and Numerical Problems

When creating an algorithm, we generally follow this process:

1. **Understand the problem** – What is given (input)? What is required (output)?
2. **Identify the steps** – Break the problem into small, simple steps.
3. **Arrange steps in order** – Steps must be in the correct sequence.
4. **Check with an example** – Mentally run through the algorithm using sample values.
5. **Refine if needed** – Fix any missing or unclear steps.

## 5. Example 1: Algorithm to Add Two Numbers

**Problem**: Find the sum of two numbers.

1. Start
2. Read two numbers, say `a` and `b`.
3. Add them: `sum = a + b`.
4. Display `sum`.
5. Stop

## 6. Example 2: Algorithm to Find the Largest of Three Numbers

**Problem**: Given three numbers `a`, `b`, `c`, find the largest one.

1. Start
2. Read three numbers `a`, `b`, `c`.
3. If `a > b` and `a > c`, then `a` is the largest.
4. Else if `b > a` and `b > c`, then `b` is the largest.
5. Else, `c` is the largest.
6. Display the largest number.
7. Stop

## 7. Example 3: Algorithm to Check if a Number is Even or Odd

**Problem**: Given a number, check whether it is even or odd.

1. Start
2. Read a number `n`.
3. Divide `n` by 2 and find the remainder (`n % 2`).
4. If remainder is `0`, then the number is **Even**.
5. Else, the number is **Odd**.
6. Display the result.
7. Stop

## 8. Example 4: Algorithm to Find the Factorial of a Number

**Problem**: Find the factorial of a number `n` (factorial = n × (n-1) × (n-2) × ... × 1).

1. Start
2. Read a number `n`.
3. Set `fact = 1`.
4. Set `i = 1`.
5. Repeat while `i <= n`:
   - `fact = fact * i`
   - `i = i + 1`
6. Display `fact`.
7. Stop

## 9. Types of Problems Algorithms Solve

- **Numerical problems**: Involve calculations (sum, average, factorial, area, etc.).
- **Logical problems**: Involve decision-making and conditions (largest number, even/odd, pass/fail, etc.).

## 10. Quick Recap (One-Line Points)

- Algorithm = step-by-step method to solve a problem.
- Written in plain, simple language — not tied to any programming language.
- Must be definite (clear), finite (must end), and effective (doable).
- Used to plan logic **before** writing actual code.
- Same algorithm can later be converted into flowchart, pseudocode, and then real code.