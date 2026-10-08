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

### Rules for Naming Variables in C (Variables are also known as Identifiers)

1. **Allowed characters:** letters (`a-z`, `A-Z`), digits (`0-9`), and underscore (`_`) only.
2. **Must start with** a letter or underscore. It cannot start with a digit.
3. **No spaces** and no special characters like `@`, `#`, `-`, `$`, `%`.
4. **Cannot be a keyword** (reserved words like `int`, `float`, `return`, `if`, `while`, `for`).
5. **Case-sensitive:** `age`, `Age`, and `AGE` are three different variables.
6. **Must be unique** within the same scope. You cannot declare two variables with the same name in the same function.
7. **No fixed length limit in practice,** but the compiler guarantees only the first 31 characters are significant. Keep names short and meaningful.

#### Valid names

c

```c
int age;
int _count;
int total2;
float student_marks;
```

#### Invalid names

c

```c
int 2total;       // starts with a digit
int total marks;  // has a space
int my-var;       // hyphen not allowed
int float;        // keyword
int price$;       // special character
```

#### Good practice (not a rule)

- Use meaningful names: `totalMarks` is better than `tm`.
- Use `camelCase` (`totalMarks`) or `snake_case` (`total_marks`) and stay consistent.
- Avoid starting with an underscore, since names like `_Bool` and `__main` are used by the compiler and libraries.



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

## 8. Testing and Debugging

### Testing vs Debugging

**Testing** is finding out *whether* there is a problem in the program.
 **Debugging** is finding out *where* the problem is and fixing it.

Testing comes first. Debugging happens only if testing finds a bug.

| Aspect            | Testing                                   | Debugging                             |
| ----------------- | ----------------------------------------- | ------------------------------------- |
| Purpose           | Check if the program works correctly      | Find the cause of an error and fix it |
| Question answered | "Is there a bug?"                         | "Where is the bug and why?"           |
| Done by           | Tester or programmer                      | Programmer                            |
| Input             | Test cases (inputs with expected outputs) | The failing test case and the code    |
| Output            | Report of pass/fail, list of defects      | Corrected code                        |
| Order             | First                                     | After testing finds a defect          |

#### Example

Program to find the average of two numbers:

c

```c
float avg = a + b / 2;   // wrong
```

- **Testing:** You run it with `a = 4, b = 6`. Expected output is `5`, but the program prints `7`. Test **fails**, so a bug exists.
- **Debugging:** You trace the code and find the problem: `/` runs before `+` (precedence). You fix it:

c

```c
float avg = (a + b) / 2.0;
```

Then you test again to confirm the fix works.

#### Quick way to remember

- Testing = **detect** the problem
- Debugging = **diagnose and cure** the problem

### Types of Operators in C

An operator is a symbol that performs an action on operands (values or variables).

#### 1. Arithmetic Operators

| Operator | Meaning             | Example | Result                 |
| -------- | ------------------- | ------- | ---------------------- |
| `+`      | Addition            | `5 + 2` | `7`                    |
| `-`      | Subtraction         | `5 - 2` | `3`                    |
| `*`      | Multiplication      | `5 * 2` | `10`                   |
| `/`      | Division            | `5 / 2` | `2` (integer division) |
| `%`      | Modulus (remainder) | `5 % 2` | `1`                    |

#### 2. Relational Operators

Compare two values. Result is `1` (true) or `0` (false).

| Operator | Meaning               | Example  | Result |
| -------- | --------------------- | -------- | ------ |
| `==`     | Equal to              | `5 == 5` | `1`    |
| `!=`     | Not equal to          | `5 != 3` | `1`    |
| `>`      | Greater than          | `5 > 3`  | `1`    |
| `<`      | Less than             | `5 < 3`  | `0`    |
| `>=`     | Greater than or equal | `5 >= 5` | `1`    |
| `<=`     | Less than or equal    | `4 <= 3` | `0`    |

Common mistake: `=` assigns a value, `==` compares. Writing `if (x = 5)` instead of `if (x == 5)` is a classic bug.

#### 3. Logical Operators

Combine conditions.

| Operator | Meaning                | Example              | Result |
| -------- | ---------------------- | -------------------- | ------ |
| `&&`     | AND (both true)        | `(5 > 3) && (2 > 1)` | `1`    |
| `||`     | OR (at least one true) | `(5 > 3) || (2 > 8)` | `1`    |
| `!`      | NOT (reverses)         | `!(5 > 3)`           | `0`    |

#### 4. Assignment Operators

| Operator | Example  | Same as        |
| -------- | -------- | -------------- |
| `=`      | `a = 5`  | store 5 in `a` |
| `+=`     | `a += 3` | `a = a + 3`    |
| `-=`     | `a -= 3` | `a = a - 3`    |
| `*=`     | `a *= 3` | `a = a * 3`    |
| `/=`     | `a /= 3` | `a = a / 3`    |
| `%=`     | `a %= 3` | `a = a % 3`    |

#### 5. Increment and Decrement Operators

| Operator | Meaning       |
| -------- | ------------- |
| `++`     | Increase by 1 |
| `--`     | Decrease by 1 |

Prefix vs postfix:

c

```c
int a = 5;
int b = ++a;   // prefix: increase first, then use → a = 6, b = 6

int c = 5;
int d = c++;   // postfix: use first, then increase → c = 6, d = 5
```

#### 6. Bitwise Operators

Work on individual bits of integers.

| Operator | Meaning         | Example (`a=5` is `0101`, `b=3` is `0011`) |
| -------- | --------------- | ------------------------------------------ |
| `&`      | AND             | `a & b` → `1`                              |
| `|`      | OR              | `a | b` → `7`                              |
| `^`      | XOR             | `a ^ b` → `6`                              |
| `~`      | NOT (flip bits) | `~a` → `-6`                                |
| `<<`     | Left shift      | `a << 1` → `10`                            |
| `>>`     | Right shift     | `a >> 1` → `2`                             |

#### 7. Conditional (Ternary) Operator

The only operator that takes **three** operands. Short form of if-else.

c

```c
result = (condition) ? value_if_true : value_if_false;

int max = (a > b) ? a : b;
```

#### 8. Special Operators

| Operator | Purpose                             | Example             |
| -------- | ----------------------------------- | ------------------- |
| `sizeof` | Size of a type or variable in bytes | `sizeof(int)` → `4` |
| `&`      | Address of a variable               | `&x`                |
| `*`      | Value at an address (pointer)       | `*p`                |
| `,`      | Comma, separates expressions        | `a = 1, b = 2`      |

`&` and `*` as address operators are used with pointers, which is a later topic.

------

### Classification by Number of Operands

| Type    | Operands | Examples                       |
| ------- | -------- | ------------------------------ |
| Unary   | 1        | `++`, `--`, `!`, `sizeof`, `~` |
| Binary  | 2        | `+`, `-`, `*`, `==`, `&&`, `=` |
| Ternary | 3        | `? :`                          |

### Precedence (High to Low, simplified)

1. `()` Highest Precedence
2. `++`, `--`, `!` (unary)
3. `*`, `/`, `%`
4. `+`, `-`
5. `<`, `<=`, `>`, `>=`
6. `==`, `!=`
7. `&&`
8. `||`
9. `? :`
10. `=`, `+=`, `-=`, etc.

For your Unit 2 syllabus, the key ones are **arithmetic, relational, logical, assignment, and increment/decrement**. Bitwise and special operators are good to know but come up less.

### 1. Expression

An expression is a combination of **operands** (variables, constants, values) and **operators** that gives a **single value**.

c

```c
a + b          // arithmetic expression
x > 10         // relational expression (result is 1 or 0)
a > 5 && b < 3 // logical expression
x = 5 + 2      // assignment expression
```

Parts of `a + b`:

- `a`, `b` are **operands**
- `+` is the **operator**

Types of expressions:

| Type       | Example              | Result                    |
| ---------- | -------------------- | ------------------------- |
| Arithmetic | `5 + 3 * 2`          | number (`11`)             |
| Relational | `5 > 3`              | `1` (true) or `0` (false) |
| Logical    | `(5 > 3) && (2 > 1)` | `1` or `0`                |
| Assignment | `x = 10`             | assigns value to `x`      |

Even a single variable or number alone (`x` or `10`) is a valid expression.

------

### 2. Literal

A literal is a **fixed value written directly in the code**.

| Type                   | Examples                         |
| ---------------------- | -------------------------------- |
| Integer literal        | `10`, `-5`, `0`                  |
| Floating-point literal | `3.14`, `-0.5`, `2.5e3` (= 2500) |
| Character literal      | `'A'`, `'7'`, `'\n'`             |
| String literal         | `"Hello"`, `"C language"`        |

Optional suffixes tell the compiler the exact type:

c

```c
100L      // long
100U      // unsigned
3.14f     // float (without f, 3.14 is a double)
```

Other number systems:

c

```c
int a = 0x1F;   // hexadecimal (31)
int b = 012;    // octal (10)
```

------

### 3. Constant

A constant is a value that **cannot change** while the program runs.

Two ways to create a named constant:

c

```c
const int MAX = 100;     // using const keyword
#define PI 3.14159        // using #define (preprocessor)
```

If you try to change it, you get a compile error:

c

```c
MAX = 200;   // ERROR: cannot assign to a const variable
```

|                 | `const` | `#define`                              |
| --------------- | ------- | -------------------------------------- |
| Has a data type | Yes     | No                                     |
| Uses memory     | Yes     | No (text is replaced before compiling) |
| Ends with `;`   | Yes     | No                                     |

------

### 4. How They Fit Together

c

```c
const int MAX = 100;
int x = 10;
int y = x + 5;
```

- `10`, `100`, `5` → **literals** (the values themselves)
- `MAX` → **constant** (a named value that cannot change)
- `x`, `y` → **variables** (can change)
- `x + 5` → **expression** (gives a value, assigned to `y`)

#### Literal vs Constant

- **Literal** = the value itself, typed directly (`100`)
- **Constant** = a name that holds a fixed value (`MAX`)

Using `MAX` instead of writing `100` everywhere is better: if the value changes, you edit it in one place only.

Want me to add this to your markdown notes?