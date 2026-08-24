# Topic 4: Representation of Algorithm — Flowchart

## 1. What is a Flowchart?

- A **flowchart** is a **diagram** that shows the steps of an algorithm using symbols and arrows.
- It gives a **visual/picture representation** of the logic, instead of writing it in plain sentences.
- Flowcharts make it easier to understand the flow of a program at a glance.

## 2. Why Use Flowcharts?

- Easy to understand, even for people who don't know programming.
- Helps in planning the logic clearly before coding.
- Useful for spotting errors or missing steps in the logic.
- Acts as documentation — helps others understand the program later.

## 3. Standard Flowchart Symbols

| Symbol Name              | Shape              | Purpose                                                      |
| ------------------------ | ------------------ | ------------------------------------------------------------ |
| **Start/End (Terminal)** | Oval/Rounded shape | Marks the beginning and end of the flowchart                 |
| **Input/Output**         | Parallelogram      | Represents input (reading data) or output (displaying data)  |
| **Process**              | Rectangle          | Represents a calculation or action (e.g., `sum = a + b`)     |
| **Decision**             | Diamond            | Represents a condition/decision with Yes/No or True/False paths |
| **Flow Line**            | Arrow              | Shows the direction/order of steps                           |
| **Connector**            | Circle             | Used to connect different parts of a flowchart, especially in large diagrams |

## 4. Rules for Drawing a Flowchart

1. Every flowchart must have **one Start** and **one End**.
2. Use arrows to clearly show the direction of flow (top to bottom, or left to right).
3. Use the **correct symbol** for each type of step (don't mix them up).
4. Decision boxes (diamonds) must have exactly two paths: **Yes/No** or **True/False**.
5. Keep it simple and neat — avoid crossing lines where possible.

![flowchart shapes meaning](https://venngage-wordpress.s3.amazonaws.com/uploads/2024/02/flowchart-symbols-meaning-1.png)

## 5. Example 1: Flowchart to Add Two Numbers

**Steps in words:**

1. Start
2. Read `a`, `b`
3. Compute `sum = a + b`
4. Display `sum`
5. Stop

**Flowchart representation (described):**

```
        ┌───────┐
        │ Start │
        └───┬───┘
            │
            ▼
   ┌───────────────────┐
   │  Read a, b          │   (Parallelogram - Input)
   └───┬─────────────────┘
       │
       ▼
   ┌───────────────────┐
   │  sum = a + b        │   (Rectangle - Process)
   └───┬─────────────────┘
       │
       ▼
   ┌───────────────────┐
   │  Display sum        │   (Parallelogram - Output)
   └───┬─────────────────┘
       │
       ▼
        ┌───────┐
        │  End  │
        └───────┘
```

## 6. Example 2: Flowchart to Find the Largest of Three Numbers

**Steps in words:**

1. Start
2. Read `a`, `b`, `c`
3. If `a > b` and `a > c` → `a` is largest
4. Else if `b > a` and `b > c` → `b` is largest
5. Else → `c` is largest
6. Display the largest number
7. Stop

**Flowchart representation (described):**

```
            ┌───────┐
            │ Start │
            └───┬───┘
                │
                ▼
        ┌───────────────┐
        │ Read a, b, c    │
        └───┬─────────────┘
            │
            ▼
       ◇──────────────◇
      ╱ Is a > b and    ╲       Yes
     ╱  a > c ?           ╲ ───────────► largest = a
      ╲                  ╱
       ◇──────────────◇
            │ No
            ▼
       ◇──────────────◇
      ╱ Is b > a and    ╲       Yes
     ╱  b > c ?           ╲ ───────────► largest = b
      ╲                  ╱
       ◇──────────────◇
            │ No
            ▼
       largest = c
            │
            ▼
    ┌───────────────────┐
    │ Display largest     │
    └───┬─────────────────┘
        │
        ▼
        ┌───────┐
        │  End  │
        └───────┘
```

*(Note: All three branches — largest = a, largest = b, largest = c — join together before "Display largest".)*

## 7. Example 3: Flowchart to Check Even or Odd

**Steps in words:**

1. Start
2. Read `n`
3. Compute `remainder = n % 2`
4. If `remainder == 0` → Display "Even"
5. Else → Display "Odd"
6. Stop

**Flowchart representation (described):**

```
        ┌───────┐
        │ Start │
        └───┬───┘
            │
            ▼
    ┌────────────────┐
    │   Read n          │
    └───┬────────────────┘
        │
        ▼
    ┌────────────────────┐
    │ remainder = n % 2     │
    └───┬────────────────────┘
        │
        ▼
   ◇──────────────◇
  ╱ remainder == 0? ╲      Yes
 ╱                    ╲ ─────────► Display "Even"
  ╲                  ╱
   ◇──────────────◇
        │ No
        ▼
   Display "Odd"
        │
        ▼
    (Both paths join)
        │
        ▼
        ┌───────┐
        │  End  │
        └───────┘
```

## 8. Advantages of Flowcharts

- Easy to understand the logic visually.
- Helps in debugging (finding logic errors) before writing code.
- Useful for communication between team members.
- Language-independent — can be converted into any programming language.

## 9. Limitations of Flowcharts

- Becomes complex and hard to draw for very large programs.
- Time-consuming to redraw if logic changes.
- No standard tool needed, but drawing by hand can be messy for big problems.

## 10. Quick Recap (One-Line Points)

- Flowchart = diagram/picture representation of an algorithm.
- Oval = Start/End, Parallelogram = Input/Output, Rectangle = Process, Diamond = Decision.
- Arrows show the flow/direction of steps.
- Every flowchart has exactly one Start and one End.
- Used to visually plan logic before writing actual code.