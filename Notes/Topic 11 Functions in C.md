# Functions in C

## 1. What is a Function?

A function is a named block of code that does one job. You write it once and call it whenever needed.

**Why use functions:**

- Avoid repeating the same code
- Break a big problem into small parts
- Easier to read, test, and debug

`main()` is also a function. Every C program starts from it.

There are two kinds:

- **Library functions** — already written for you (`printf`, `scanf`, `strlen`, `sqrt`)
- **User-defined functions** — written by you

------

## 2. Three Parts of a Function

### a) Declaration (Prototype)

Tells the compiler that the function exists. Written before `main()`.

```c
int add(int a, int b);
```

### b) Definition

The actual code of the function.

```c
int add(int a, int b) {
    return a + b;
}
```

### c) Call

Using the function.

```c
int result = add(5, 3);
```

### Full Example

```c
#include <stdio.h>

int add(int a, int b);        // declaration

int main() {
    int result = add(5, 3);   // call
    printf("%d\n", result);   // 8
    return 0;
}

int add(int a, int b) {       // definition
    return a + b;
}
```

If you write the definition *above* `main()`, the declaration is not needed.

------

## 3. Syntax

```c
return_type function_name(parameter_list) {
    // body
    return value;
}
```

| Part             | Meaning                                                  |
| ---------------- | -------------------------------------------------------- |
| `return_type`    | Type of value sent back (`int`, `float`, `char`, `void`) |
| `function_name`  | Name you choose (same rules as variable names)           |
| `parameter_list` | Inputs the function receives (can be empty)              |
| `return`         | Sends the value back and ends the function               |

**Parameters vs Arguments**

- **Parameters** — variables in the function definition: `int a, int b`
- **Arguments** — actual values passed in the call: `add(5, 3)`

------

## 4. Four Types of Functions

### 1. No parameters, no return value

```c
void hello() {
    printf("Hello!\n");
}
```

Call: `hello();`

### 2. With parameters, no return value

```c
void greet(char name[]) {
    printf("Hello, %s!\n", name);
}
```

Call: `greet("Ananya");`

### 3. No parameters, with return value

```c
int getFive() {
    return 5;
}
```

Call: `int x = getFive();`

### 4. With parameters, with return value

```c
int square(int n) {
    return n * n;
}
```

Call: `int x = square(4);`   // 16

------

## 5. The `return` Statement

- Sends a value back to the caller
- Ends the function immediately — code after `return` does not run
- A `void` function does not return a value
- A function can return only **one** value

```c
int max(int a, int b) {
    if (a > b)
        return a;
    return b;
}
```

------

## 6. Pass by Value

C sends a **copy** of the argument to the function. Changing the parameter inside the function does **not** change the original variable.

```c
void increment(int x) {
    x = x + 1;
}

int main() {
    int num = 5;
    increment(num);
    printf("%d", num);   // 5, not 6
    return 0;
}
```

To change the original variable, you need pointers (a later topic).

------

## 7. Scope and Lifetime of Variables

| Type         | Where declared                   | Visible in         | Lives until                        |
| ------------ | -------------------------------- | ------------------ | ---------------------------------- |
| Local        | Inside a function                | That function only | Function ends                      |
| Global       | Outside all functions            | Whole file         | Program ends                       |
| Static local | Inside a function, with `static` | That function only | Program ends (value is remembered) |

```c
int total = 0;          // global

void addToTotal(int n) {
    int temp = n;        // local
    total = total + temp;
}

void counter() {
    static int count = 0;   // remembers value between calls
    count++;
    printf("%d\n", count);
}
```

Two different functions can use the same local variable name. They do not affect each other.

------

## 8. Passing an Array to a Function

When you pass an array, the function works on the **original array**, not a copy. So changes made inside the function stay.

```c
void doubleAll(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] = arr[i] * 2;
    }
}

int main() {
    int marks[3] = {1, 2, 3};
    doubleAll(marks, 3);
    // marks is now {2, 4, 6}
    return 0;
}
```

Always pass the size as a separate argument. The function cannot find the array size by itself.

------

## 9. Recursion

A function that calls itself. It needs:

1. **Base case** — when to stop
2. **Recursive case** — the function calls itself with a smaller problem

```c
int factorial(int n) {
    if (n == 0 || n == 1)       // base case
        return 1;
    return n * factorial(n - 1); // recursive case
}
```

How `factorial(3)` works:

```
factorial(3) = 3 * factorial(2)
             = 3 * 2 * factorial(1)
             = 3 * 2 * 1
             = 6
```

Without a base case, the function calls itself forever and the program crashes.

------

## 10. Example: Prime Number Function

```c
#include <stdio.h>

int isPrime(int n) {
    if (n <= 1)
        return 0;

    for (int i = 2; i < n; i++) {
        if (n % i == 0)
            return 0;      // divisor found, not prime
    }
    return 1;              // no divisor found, prime
}

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);

    if (isPrime(num))
        printf("%d is prime.\n", num);
    else
        printf("%d is NOT prime.\n", num);

    return 0;
}
```

In classic C there is no boolean type, so functions return `1` for true and `0` for false. From C99 you can use `bool` with `#include <stdbool.h>`.

### First N prime numbers using the function

```c
int main() {
    int N, count = 0, num = 2;
    scanf("%d", &N);

    while (count < N) {
        if (isPrime(num)) {
            printf("%d ", num);
            count++;
        }
        num++;
    }
    return 0;
}
```

------

## 11. Common Mistakes

1. **Missing declaration** — calling a function before `main()` knows about it
2. **Wrong return type** — function says `int` but returns nothing
3. **Wrong number or type of arguments** in the call
4. **Expecting the original variable to change** after pass by value
5. **Recursion without a base case**
6. **Missing semicolon** at the end of the declaration (`int add(int a, int b);`)

------

## 12. Practice Questions

1. Write a function `isEven(int n)` that returns 1 if `n` is even, 0 otherwise.
2. Write a function `power(base, exp)` without using `pow()`.
3. Write a function to find the largest of three numbers.
4. Write separate functions for add, subtract, multiply, divide and call them using a menu.
5. Write a recursive function to find the sum of first N natural numbers.
6. Write a function that returns the reverse of a number.
7. Write a function to print all primes between 1 and 100 using `isPrime()`.