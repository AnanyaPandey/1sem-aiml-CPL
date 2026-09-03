# Characters, Strings, Control Structures, and Functions in C

## 1. Characters (`char`)

A `char` stores a single character, using single quotes.

```c
char grade = 'A';
char symbol = '$';
char digit = '7';        // this is the character '7', NOT the number 7
```

Internally, a `char` is just a small integer (1 byte). Every character has a numeric code behind it (ASCII).

```c
char c = 'A';
printf("%d", c);     // prints 65 (ASCII code of 'A')

int x = 65;
printf("%c", x);     // prints A
```

Common ASCII points to know: `'A'` = 65, `'a'` = 97, `'0'` = 48.

This lets you do character arithmetic:

```c
char c = 'A';
c = c + 1;
printf("%c", c);     // prints B
```

------

## 2. Strings (recap)

No built-in string type in C — just a `char` array ending in `'\0'` (null terminator).

```c
char name[] = "Ananya";   // 'A','n','a','n','y','a','\0'
```

------

## 3. String Methods (`<string.h>`)

| Function                | Purpose                          | Example                 |
| ----------------------- | -------------------------------- | ----------------------- |
| `strlen(s)`             | returns length (excludes `'\0'`) | `strlen("Hi")` → `2`    |
| `strcpy(dest, src)`     | copies `src` into `dest`         | `strcpy(a, "Hi")`       |
| `strncpy(dest, src, n)` | copies max `n` chars             | `strncpy(a, "Hi", 1)`   |
| `strcat(dest, src)`     | appends `src` to end of `dest`   | `strcat(a, "Bye")`      |
| `strncat(dest, src, n)` | appends max `n` chars            |                         |
| `strcmp(s1, s2)`        | compares; `0` if equal           | `strcmp("a","a")` → `0` |
| `strchr(s, ch)`         | finds first occurrence of `ch`   | `strchr("Hi","i")`      |
| `strstr(s1, s2)`        | finds `s2` inside `s1`           | `strstr("Hello","ell")` |

```c
#include <stdio.h>
#include <string.h>

int main() {
    char a[20] = "Hello";
    char b[] = "World";

    printf("Length: %lu\n", strlen(a));       // 5

    strcat(a, b);
    printf("Concat: %s\n", a);                 // HelloWorld

    if (strcmp("cat", "cat") == 0)
        printf("Strings are equal\n");

    return 0;
}
```

Note: `strcpy`/`strcat` don't check array size for you. If `dest` isn't big enough, you get memory corruption — a very common C bug.

------

## 4. Control Structures

### if / else

```c
int marks = 75;

if (marks >= 90) {
    printf("Grade A\n");
} else if (marks >= 60) {
    printf("Grade B\n");
} else {
    printf("Grade C\n");
}
```

- Condition goes inside `()`.
- Braces `{}` group multiple statements. If only one statement, `{}` is optional (but recommended for clarity).
- `else if` chains let you check multiple conditions in order — the first `true` one runs, rest are skipped.

### Comparison / logical operators used in conditions

| Operator             | Meaning      |
| -------------------- | ------------ |
| `==`                 | equal to     |
| `!=`                 | not equal to |
| `>`, `<`, `>=`, `<=` | comparisons  |
| `&&`                 | logical AND  |
| `||`                 | logical OR   |
| `!`                  | logical NOT  |

```c
if (age >= 18 && hasID == 1) {
    printf("Allowed\n");
}
```

------

## 5. for Loop

Syntax:

```c
for (initialization; condition; update) {
    // body
}
for (int i = 1; i <= 5; i++) {
    printf("%d\n", i);
}
```

Execution order:

1. `initialization` runs **once** (`int i = 1`)
2. `condition` is checked (`i <= 5`) — if false, loop ends
3. `body` runs
4. `update` runs (`i++`)
5. go back to step 2, repeat

Example — sum of first 5 numbers:

```c
int sum = 0;
for (int i = 1; i <= 5; i++) {
    sum = sum + i;
}
printf("Sum = %d\n", sum);   // 15
```

Looping over a char array:

```c
char name[] = "Ananya";
for (int i = 0; name[i] != '\0'; i++) {
    printf("%c\n", name[i]);
}
```

------

## 6. Functions

A function is a named, reusable block of code.

### Declaration (prototype) and Definition

```c
// Function declaration (prototype) — tells compiler it exists, goes before main()
int add(int a, int b);

int main() {
    int result = add(5, 3);      // function call
    printf("%d\n", result);      // 8
    return 0;
}

// Function definition — the actual code
int add(int a, int b) {
    int sum = a + b;
    return sum;
}
```

### Anatomy of a function

```c
return_type function_name(parameter_list) {
    // body
    return value;   // must match return_type (skip if void)
}
```

- **return_type**: data type of the value it sends back (`int`, `float`, `char`, or `void` for nothing)
- **parameters**: inputs passed in (can be zero or more)
- **return**: sends a value back and exits the function immediately

### Function with no return value

```c
void greet(char name[]) {
    printf("Hello, %s!\n", name);
    // no return needed
}

int main() {
    greet("Ananya");
    return 0;
}
```

### Function with no parameters

```c
int getFive() {
    return 5;
}
```

### Why use functions

- Avoid repeating code
- Break a big problem into smaller, testable pieces
- Easier to read and debug

### Parameter passing in C: pass by value

```c
void increment(int x) {
    x = x + 1;          // this changes only the local copy
}

int main() {
    int num = 5;
    increment(num);
    printf("%d", num);   // still 5, NOT 6
    return 0;
}
```

C passes a **copy** of the variable, not the original. To actually modify the caller's variable, you need pointers — `void increment(int *x) { *x = *x + 1; }`.

------

## 7. Format Specifiers in C (`printf` / `scanf`)

Used with `printf()` to display values and `scanf()` to read input — they tell C how to interpret the bytes in memory.

### Integer Types

| Specifier   | Type                     | Example                          |
| ----------- | ------------------------ | -------------------------------- |
| `%d` / `%i` | `int`                    | `printf("%d", 10);`              |
| `%u`        | `unsigned int`           | `printf("%u", 10u);`             |
| `%hd`       | `short int`              |                                  |
| `%hu`       | `unsigned short int`     |                                  |
| `%ld`       | `long int`               | `printf("%ld", 100000L);`        |
| `%lu`       | `unsigned long int`      |                                  |
| `%lld`      | `long long int`          | `printf("%lld", 10000000000LL);` |
| `%llu`      | `unsigned long long int` |                                  |

### Floating Point Types

| Specifier   | Type                                                         | Example                                      |
| ----------- | ------------------------------------------------------------ | -------------------------------------------- |
| `%f`        | `float` (also works for `double` in `printf`)                | `printf("%f", 3.14);`                        |
| `%lf`       | `double` — **required** for `scanf`, optional (same as `%f`) in `printf` | `scanf("%lf", &d);`                          |
| `%Lf`       | `long double`                                                |                                              |
| `%e` / `%E` | scientific notation                                          | `printf("%e", 12345.6789);` → `1.234568e+04` |
| `%g` / `%G` | shortest of `%f` or `%e`                                     |                                              |

**Gotcha:** in `printf`, `%f` and `%lf` behave the same (both print a `double`, since `float` args are auto-promoted). But in `scanf`, you **must** use `%f` for a `float*` and `%lf` for a `double*` — mixing these up is a classic bug.

### Character and String

| Specifier | Type                | Example               |
| --------- | ------------------- | --------------------- |
| `%c`      | single `char`       | `printf("%c", 'A');`  |
| `%s`      | string (char array) | `printf("%s", name);` |

### Pointer / Address

| Specifier | Type                     | Example             |
| --------- | ------------------------ | ------------------- |
| `%p`      | pointer / memory address | `printf("%p", &x);` |

### Other / Miscellaneous

| Specifier | Type                             | Example                       |
| --------- | -------------------------------- | ----------------------------- |
| `%x`      | unsigned hex (lowercase)         | `printf("%x", 255);` → `ff`   |
| `%X`      | unsigned hex (uppercase)         | `printf("%X", 255);` → `FF`   |
| `%o`      | unsigned octal                   | `printf("%o", 8);` → `10`     |
| `%%`      | prints a literal `%`             | `printf("100%%");` → `100%`   |
| `%zu`     | `size_t` (what `sizeof` returns) | `printf("%zu", sizeof(int));` |

### Width, Precision, Flags (formatting output)

```c
printf("%5d", 42);       // pads to width 5:      "   42"
printf("%-5d|", 42);     // left-align:            "42   |"
printf("%05d", 42);      // pad with zeros:        "00042"
printf("%.2f", 3.14159); // 2 decimal places:      "3.14"
printf("%8.2f", 3.14159);// width 8, 2 decimals:   "    3.14"
```

### Example Using Several Together

```c
#include <stdio.h>

int main() {
    int a = 10;
    unsigned int b = 20;
    long c = 100000L;
    float d = 3.14f;
    double e = 3.14159265;
    char ch = 'A';
    char name[] = "Ananya";

    printf("%d %u %ld %f %lf %c %s\n", a, b, c, d, e, ch, name);
    printf("Hex: %x, Octal: %o, Pointer: %p\n", 255, 8, (void*)&a);

    return 0;
}
```