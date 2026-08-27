# C Programming Basics

## 1. Compiler vs Interpreter

| Aspect          | Compiler                                                     | Interpreter                                          |
| --------------- | ------------------------------------------------------------ | ---------------------------------------------------- |
| Translation     | Converts entire source code to machine code before execution | Translates and executes line-by-line                 |
| Speed           | Faster execution (translation done once)                     | Slower (translates every time it runs)               |
| Error detection | Shows all errors after full compilation                      | Stops at first error                                 |
| Output          | Creates a separate executable file (.exe)                    | No separate executable; needs interpreter every time |
| Examples        | C, C++                                                       | Python, older BASIC implementations                  |

**C is a compiled language.**

Flow: `Source Code (.c)` → `Compiler` → `Object Code` → `Linker` (adds library code) → `Executable (.exe)` → `Run`

------

## 2. Basic Structure of a C Program

```c
#include <stdio.h>      // Preprocessor directive - includes header file

int main() {            // main function - execution starts here
    // declarations
    int a;

    // statements
    a = 5;
    printf("%d", a);

    return 0;            // returns 0 to OS - success
}
```

Parts, in order:

1. **Preprocessor directives** (`#include`) — pull in libraries like `stdio.h` for input/output
2. **main() function** — every C program must have exactly one; execution always starts here
3. **Variable declarations**
4. **Statements/expressions** — the actual logic
5. **return statement** — ends the function, sends a status code back

------

## 3. Variable Declaration

Syntax: `data_type variable_name;`

```c
int age;                // single variable
int a, b, c;             // multiple variables, same type
int x = 10;               // declaration + initialization
float pi = 3.14;
char grade = 'A';
```

### Rules for naming variables (identifiers)

- Must start with a letter or underscore (`_`), not a digit
- Can contain letters, digits, underscores
- Cannot use C keywords (`int`, `float`, `return`, etc.)
- Case-sensitive (`age` and `Age` are different)
- No spaces or special characters (`@`, `-`, etc.)

------

## 4. Basic Data Types

| Type      | Keyword  | Size (typical) | Example                                |
| --------- | -------- | -------------- | -------------------------------------- |
| Integer   | `int`    | 4 bytes        | `int x = 10;`                          |
| Float     | `float`  | 4 bytes        | `float pi = 3.14;`                     |
| Double    | `double` | 8 bytes        | `double d = 3.14159;`                  |
| Character | `char`   | 1 byte         | `char c = 'A';`                        |
| No value  | `void`   | —              | used for functions that return nothing |

Modifiers you'll also see: `short`, `long`, `signed`, `unsigned` — e.g. `unsigned int`, `long int`.

------

## 5. Constants and Literals

```c
const int MAX = 100;      // constant - value can't change
#define PI 3.14159          // macro constant (preprocessor)
```

------

## 6. How Memory Is Allocated for Variables in C

When a program runs, the operating system gives it a chunk of memory. This memory is divided into segments:

| Segment             | What is stored there                                         |
| ------------------- | ------------------------------------------------------------ |
| Code / Text segment | The compiled machine instructions of the program             |
| Data segment        | Global and static variables that are initialized             |
| BSS segment         | Global and static variables that are **not** initialized (default to 0) |
| Stack               | Local variables, function parameters, return addresses       |
| Heap                | Memory allocated dynamically at run time (`malloc`, `calloc`, etc.) |

### What happens when you declare a variable

```c
int x;
```

- The compiler looks at the data type (`int`) and knows how many bytes to reserve — typically 4 bytes for `int`.
- It reserves that many bytes **on the stack** (if it's a local variable inside a function) and creates a mapping: the name `x` refers to that memory address.
- No value is guaranteed to be there until you assign one — it holds whatever garbage value was left in that memory location before.

```c
int x = 10;
```

- Same memory reservation happens, but the compiler also generates an instruction to store `10` into that memory address immediately.

### Size in memory depends on data type

| Data type | Typical size | Bytes reserved |
| --------- | ------------ | -------------- |
| `char`    | 1 byte       | 1              |
| `int`     | 4 bytes      | 4              |
| `float`   | 4 bytes      | 4              |
| `double`  | 8 bytes      | 8              |

You can verify this yourself using the `sizeof()` operator:

```c
printf("%zu", sizeof(int));   // prints 4 (on most systems)
```

### Where the variable lives

- **Local variable** (declared inside a function, like inside `main()`) → allocated on the **stack**. Memory is automatically freed when the function ends.
- **Global variable** (declared outside all functions) → allocated in the **data** or **BSS** segment. Memory exists for the entire life of the program.
- **Dynamically allocated memory** (using `malloc`, `calloc` in `stdlib.h`) → allocated on the **heap**. Memory stays until you explicitly free it with `free()`, or the program ends.

```c
int *p = (int *) malloc(sizeof(int));   // reserves 4 bytes on the heap
*p = 25;                                 // stores 25 there
free(p);                                 // releases that memory back
```

### Every variable has an address

You can see the memory address a variable is stored at using the `&` (address-of) operator:

```c
int x = 5;
printf("%p", &x);   // prints the memory address of x, e.g. 0x7ffee4c5a9ac
```

This is also why `scanf` needs `&` before variable names — it needs the memory address to know *where* to write the input value.

------

## 7. Simple Example Program

```c
#include <stdio.h>

int main() {
    int num1, num2, sum;

    printf("Enter two numbers: ");
    scanf("%d %d", &num1, &num2);

    sum = num1 + num2;

    printf("Sum = %d\n", sum);

    return 0;
}
```

- `printf` — output
- `scanf` — input (note the `&` before variable names — it passes the memory address)
- `%d` — format specifier for `int` (use `%f` for float, `%c` for char, `%lf` for double)