# Arrays in C

An array is a collection of elements of the **same data type**, stored in contiguous memory locations.

## 1. Declaration

Syntax: `data_type array_name[size];`

```c
int marks[5];          // array of 5 integers
float prices[10];      // array of 10 floats
```

- `size` must be a constant (known at compile time for a normal array).
- Memory reserved = `size × sizeof(data_type)`. For `int marks[5]`, that's `5 × 4 = 20 bytes`, all contiguous on the stack (if local).

## 2. Declaration with Initialization

```c
int marks[5] = {90, 85, 78, 92, 88};

int marks[] = {90, 85, 78, 92, 88};   // size auto-determined as 5

int marks[5] = {90, 85};              // remaining elements auto-set to 0 → {90, 85, 0, 0, 0}
```

## 3. Accessing Elements

Indexing starts at **0**.

```c
int marks[5] = {90, 85, 78, 92, 88};

printf("%d", marks[0]);   // 90 (first element)
printf("%d", marks[4]);   // 88 (last element)

marks[2] = 100;            // modify third element
```

Valid indices are `0` to `size-1`. `marks[5]` here would be **out of bounds** — C doesn't check this for you, so it can silently corrupt memory.

## 4. Looping Through an Array

```c
int marks[5] = {90, 85, 78, 92, 88};

for (int i = 0; i < 5; i++) {
    printf("%d\n", marks[i]);
}
```

## 5. Memory Layout

Array elements sit **back to back** in memory. If `marks` starts at address `1000` and each `int` is 4 bytes:

| Index   | 0    | 1    | 2    | 3    | 4    |
| ------- | ---- | ---- | ---- | ---- | ---- |
| Address | 1000 | 1004 | 1008 | 1012 | 1016 |
| Value   | 90   | 85   | 78   | 92   | 88   |

The array name itself (`marks`) acts like a pointer to the first element's address (`&marks[0]`).

------

# Char Arrays (Strings in C)

**C has no built-in `string` data type.** A "string" in C is just a **convention**: an array of `char`, ending with the null character `'\0'` to mark where it stops.

- In languages like Python, Java, or C++, `string` is a real type you can declare.
- In C, `char name[] = "Ananya";` is not a "string object" — it's a plain `char` array, and the compiler auto-adds `'\0'` at the end and lets you use `%s` in `printf`/`scanf` to treat it as text.

This is why:

- There's no `strlen()` built into the language itself — it's a **library function** in `<string.h>` that walks the array counting characters until it hits `'\0'`.
- You can't do `str1 + str2` to join two strings like in Python/Java — there's no string type to overload `+` for. You need `strcat()` instead.
- Copying strings needs `strcpy()`, not a simple `=` assignment (arrays can't be assigned directly with `=` in C except at declaration).

**Mental model:** *"String" in C = a char array + the discipline of ending it with `'\0'` + library functions in `string.h` that respect that convention.*

If you forget the `'\0'` (e.g., you build a char array manually without it), C has no idea where the "string" ends, and functions like `printf("%s", ...)` will read past your array into random memory — a classic C bug.

## 1. Declaration

```c
char name[10];                         // uninitialized char array
char name[10] = "Ananya";              // string literal init
char name[] = "Ananya";                // size auto-determined = 7 (6 letters + '\0')
char name[7] = {'A','n','a','n','y','a', '\0'}; // manual, char by char - needs 7, not 6!
```

**Important:** `"Ananya"` has 6 visible characters, but needs **7 bytes** — the last one is the automatically-added `'\0'` (null terminator), which marks "string ends here."

## 2. Why the Null Terminator Matters

```c
char name[] = "Hi";   // stored as: 'H', 'i', '\0'  → 3 bytes
```

Functions like `printf("%s", name)` keep reading characters until they hit `'\0'`. Without it, `printf` would keep reading garbage memory past the array.

## 3. Accessing Characters

```c
char name[] = "Ananya";

printf("%c", name[0]);   // 'A'
printf("%s", name);      // "Ananya"  -- %s prints whole string till '\0'
```

## 4. Input for Char Arrays

```c
char name[20];
scanf("%s", name);          // NOTE: no '&' needed - array name is already an address
```

- `%s` with `scanf` stops reading at the first whitespace (so it can't capture multi-word input like "Ananya Pandey").
- For full lines with spaces, use `fgets(name, 20, stdin);` instead.

## 5. Common String Functions (`<string.h>`)

| Function            | Purpose                  | Example                  |
| ------------------- | ------------------------ | ------------------------ |
| `strlen(s)`         | length (excludes `'\0'`) | `strlen("Hi")` → 2       |
| `strcpy(dest, src)` | copy string              | `strcpy(name, "Ravi")`   |
| `strcat(dest, src)` | concatenate              | `strcat(greeting, name)` |
| `strcmp(s1, s2)`    | compare (0 if equal)     | `strcmp("a","a")` → 0    |

## 6. Full Example

```c
#include <stdio.h>
#include <string.h>

int main() {
    char name[20];

    printf("Enter your name: ");
    scanf("%s", name);

    printf("Hello, %s! Your name has %lu letters.\n", name, strlen(name));

    return 0;
}
```