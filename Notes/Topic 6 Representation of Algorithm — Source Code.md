# Topic 6: Representation of Algorithm — Source Code

## 1. What is Source Code?

- **Source code** is the actual program written in a specific programming language (like C) that follows **strict syntax rules**.
- Unlike pseudocode, source code **must** follow the exact grammar/rules of the language, or it will not compile/run.
- Source code is the **final step** — it converts our planned logic (algorithm → flowchart → pseudocode) into a real, working program.

## 2. From Algorithm to Source Code — The Full Journey

| Stage          | Form                            | Example                                                 |
| -------------- | ------------------------------- | ------------------------------------------------------- |
| 1. Algorithm   | Plain English steps             | "Add a and b, display sum"                              |
| 2. Flowchart   | Diagram with symbols            | Oval → Parallelogram → Rectangle → Parallelogram → Oval |
| 3. Pseudocode  | Code-like, no strict syntax     | `sum = a + b` `DISPLAY sum`                             |
| 4. Source Code | Actual C program, strict syntax | `sum = a + b;` `printf("%d", sum);`                     |

This shows how the same problem is represented in increasing levels of detail and technicality, ending in real code that a computer can run.

## 3. Basic Structure of a C Program

```c
#include <stdio.h>      // Header file - gives access to input/output functions

int main() {            // main() - every C program starts execution from here
    // statements go here
    return 0;            // tells the OS the program ended successfully
}
```

### Explanation of Each Part

- `#include <stdio.h>` – Includes the **Standard Input Output** library, which gives us functions like `printf` (to display output) and `scanf` (to take input).
- `int main()` – The **main function**. Execution of every C program begins here.
- `{ }` (curly braces) – Mark the beginning and end of a block of code.
- `return 0;` – Ends the `main` function and tells the operating system that the program finished without errors.
- `;` (semicolon) – Every statement in C must end with a semicolon.

## 4. Example 1: Source Code to Add Two Numbers

```c
#include <stdio.h>

int main() {
    int a, b, sum;

    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);

    sum = a + b;

    printf("Sum = %d\n", sum);

    return 0;
}
```

### Line-by-Line Explanation

- `int a, b, sum;` – Declares three variables of type integer.
- `printf("Enter two numbers: ");` – Displays a message asking for input.
- `scanf("%d %d", &a, &b);` – Reads two integer values from the user and stores them in `a` and `b`. The `&` symbol means "address of" — it tells C where to store the value in memory.
- `sum = a + b;` – Adds the two numbers and stores the result in `sum`.
- `printf("Sum = %d\n", sum);` – Displays the result. `%d` is a placeholder for an integer value.

## 5. Example 2: Source Code to Find the Largest of Three Numbers

```c
#include <stdio.h>

int main() {
    int a, b, c;

    printf("Enter three numbers: ");
    scanf("%d %d %d", &a, &b, &c);

    if (a > b && a > c) {
        printf("Largest number is %d\n", a);
    }
    else if (b > a && b > c) {
        printf("Largest number is %d\n", b);
    }
    else {
        printf("Largest number is %d\n", c);
    }

    return 0;
}
```

### Key Points

- `if`, `else if`, `else` – Used for decision-making, directly matching the pseudocode's `IF-ELSE IF-ELSE` structure.
- `&&` – Means "AND" in C (both conditions must be true).

## 6. Example 3: Source Code to Check Even or Odd

```c
#include <stdio.h>

int main() {
    int n, remainder;

    printf("Enter a number: ");
    scanf("%d", &n);

    remainder = n % 2;

    if (remainder == 0) {
        printf("%d is Even\n", n);
    }
    else {
        printf("%d is Odd\n", n);
    }

    return 0;
}
```

### Key Points

- `%` – The **modulus operator** in C, gives the remainder after division. This directly matches `MOD` used in pseudocode.
- `==` – Used to **compare** two values (not to be confused with `=`, which **assigns** a value).

## 7. Example 4: Source Code to Find Factorial of a Number

```c
#include <stdio.h>

int main() {
    int n, i;
    long int fact = 1;

    printf("Enter a number: ");
    scanf("%d", &n);

    for (i = 1; i <= n; i++) {
        fact = fact * i;
    }

    printf("Factorial = %ld\n", fact);

    return 0;
}
```

### Key Points

- `for (i = 1; i <= n; i++)` – A loop that repeats steps a fixed number of times, matching the pseudocode's `WHILE i <= n DO`.
- `long int` – Used because factorial values can become very large, very quickly.

## 8. Comparing Pseudocode and Source Code Side-by-Side

**Pseudocode:**

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

**C Source Code:**

```c
#include <stdio.h>
int main() {
    int n, remainder;
    scanf("%d", &n);
    remainder = n % 2;
    if (remainder == 0) {
        printf("Even");
    } else {
        printf("Odd");
    }
    return 0;
}
```

Notice how closely they match — the logic is identical; only the syntax has become strict and language-specific.

## 9. Why Learn All Four Representations?

- **Algorithm** – Helps you think through the problem in plain language.
- **Flowchart** – Helps you visualize the flow of logic.
- **Pseudocode** – Helps you structure the logic close to real code, without worrying about syntax.
- **Source Code** – The final, working program that the computer can actually compile and run.

Together, these four steps form a complete process: **Understand → Plan → Structure → Implement.**

## 10. Quick Recap (One-Line Points)

- Source code = actual program written in a real language (e.g., C), following strict syntax.
- Every C program starts execution from `main()`.
- `#include <stdio.h>` gives access to input/output functions like `printf` and `scanf`.
- Every statement in C ends with a semicolon `;`.
- Source code is the final, executable form of an algorithm — after Algorithm → Flowchart → Pseudocode → Source Code.