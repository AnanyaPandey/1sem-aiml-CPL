# Memory Locations, Object/Executable Code, and Arithmetic Expressions

## 1. Memory Locations

### The Building Analogy

Think of RAM as a huge apartment building with millions of numbered rooms, each 1 byte in size. Declaring a variable reserves actual rooms and puts a name tag on the door.

```c
int x = 10;
```

This reserves 4 consecutive bytes (since `int` needs 4 bytes), writes `10` into them, and lets you refer to that spot as `x`.

### The Memory Segments

| Segment       | Analogy (Simplified Example)                          | What lives there                                           |
| ------------- | ----------------------------------------------------- | ---------------------------------------------------------- |
| **Code/Text** | The building's blueprint framed on the wall           | Compiled instructions (your program logic)                 |
| **Data**      | A permanently rented, pre-furnished room              | Global/static variables that were **initialized**          |
| **BSS**       | A permanently rented, empty room                      | Global/static variables **not initialized** (default to 0) |
| **Stack**     | A hotel — rooms booked and vacated constantly         | Local variables inside functions, parameters               |
| **Heap**      | An open plot of land you request rooms from as needed | Memory requested manually (`malloc`)                       |

### Local Variable → Stack

```c
int main() {
    int x = 10;   // reserved on the stack
    return 0;
}   // room automatically vacated when main() ends
```

Like a hotel room: booked at check-in (function start), automatically cleared at check-out (function end) — no manual cleanup needed.

### Global Variable → Data or BSS

Both Data and BSS hold variables that live for the **entire program** (globals and `static` variables) — the difference is whether a starting value was given.

**Data segment** — initialized global/static variables. Since a real value is given, that value must be stored in the executable file itself, ready the moment the program loads.

```c
int total = 50;     // Data segment
static int c = 5;   // Data segment
```

**BSS segment** — uninitialized global/static variables. C guarantees these start at 0, so the compiler doesn't need to store actual zero-bytes in the executable — it just notes "reserve this much space and zero it out" at load time. This saves disk space in the executable file.

```c
int count;           // BSS segment (defaults to 0)
static int d;         // BSS segment (defaults to 0)
```

**Important:** a local variable inside a function — even if initialized — is NOT Data/BSS. It's on the Stack, because Data/BSS is only for variables that exist for the whole program's lifetime.

```c
int a = 10;      // Data segment (global, initialized)
int b;            // BSS segment (global, uninitialized)

int main() {
    int x = 10;    // Stack — local, not Data/BSS, even though initialized
    return 0;
}
```

### Dynamic Memory → Heap

```c
int *p = (int *) malloc(sizeof(int));   // explicitly request a room
*p = 25;
free(p);                                 // explicitly give it back
```

Like renting a plot of land yourself — nobody reclaims it automatically. Forgetting `free()` causes a **memory leak**: the room stays "occupied" forever even after you're done with it.

### Seeing the Address

```c
int x = 5;
printf("%p", &x);   // prints something like 0x7ffee4c5a9ac — the "room number"
```

`&` = "address of" — gives the room number, not the value inside. This is why `scanf` needs `&`:

```c
scanf("%d", &num1);   // "go to this room number and write the value there directly"
```

------

## 2. Object Code and Executable Code

### The Recipe Book Analogy

Source code (`.c` file) is a recipe book written in a language only you understand. Construction robots (the CPU) only understand raw machine commands, so the recipe must be translated — in stages.

### Stage 1: Source Code (`.c`)

Human-readable C code.

```c
#include <stdio.h>
int main() {
    printf("Hello");
    return 0;
}
```

### Stage 2: Compilation → Object Code (`.o` / `.obj`)

The compiler translates source code into machine code — but it's **not runnable yet**. Calling `printf()` doesn't include the actual compiled code for `printf` — that lives in a separate pre-built library. The object code has your logic plus a placeholder note: *"I need the real code for `printf` — plug it in later."*

**Analogy:** a pre-built room with walls and wiring done, but a gap left for the front door and a sticky note reading "insert standard door #402 here."

### Stage 3: Linking → Executable Code (`.exe` / `a.out`)

The **linker** takes the object code, finds the missing pieces (like the compiled `printf` code from the C standard library), and stitches everything into one complete, self-contained file — the **executable**.

**Analogy:** the contractor grabs standard door #402 from the warehouse and bolts it into the gap. The house is now complete and livable.

### The Full Pipeline

```
Source Code (.c)
      │  compiler translates code, leaves gaps for library functions
      ▼
Object Code (.o)  ─── one object file per source file, if multiple .c files
      │  linker fills gaps with library code, merges multiple .o files
      ▼
Executable Code (.exe)
      │  loaded into memory by the OS
      ▼
Program Running
```

### Why Two Steps?

- **Separate compilation:** in a project with 10 `.c` files, editing one file means only that file needs recompiling — not all 10 — before re-linking. Saves time on large projects.
- **Reusability:** library functions like `printf` are compiled once and reused by every program that links against them, instead of being rewritten from scratch each time.

### On the Command Line (gcc)

```bash
gcc -c hello.c        # stops after compiling → produces hello.o (object code)
gcc hello.o -o hello  # links → produces hello (executable)

gcc hello.c -o hello  # does BOTH steps in one command (most common)
```

- `hello.o` — object code, not directly runnable, has unresolved references to library functions
- `hello` (or `hello.exe` on Windows) — executable, runnable directly: `./hello`

------

## 3. Arithmetic Expressions

An arithmetic expression combines variables, constants, and operators to produce a numeric value.

```c
int result = 5 + 3 * 2;
```

### The Operators

| Operator | Meaning             | Example | Result                  |
| -------- | ------------------- | ------- | ----------------------- |
| `+`      | addition            | `5 + 3` | `8`                     |
| `-`      | subtraction         | `5 - 3` | `2`                     |
| `*`      | multiplication      | `5 * 3` | `15`                    |
| `/`      | division            | `5 / 2` | `2` (integer division!) |
| `%`      | modulus (remainder) | `5 % 2` | `1`                     |

### The Integer Division Trap

```c
int a = 5 / 2;      // a = 2, NOT 2.5 — both operands are int, result truncates
float b = 5 / 2;     // b = 2.0 — still truncates! Division happens BEFORE assignment
float c = 5.0 / 2;   // c = 2.5 — works, because one operand is now a float
```

**Rule:** if both operands are integers, `/` gives integer division (decimal part discarded, not rounded). For a decimal answer, at least one operand must be `float`/`double`.

### Modulus (`%`)

Only works with integers — gives the remainder.

```c
printf("%d", 7 % 3);   // 1  (7 = 2*3 + 1)
printf("%d", 10 % 5);  // 0  (10 divides evenly)
```

Common use: checking even/odd with `if (x % 2 == 0)`.

------

## 4. Precedence and Associativity

Like BODMAS/PEMDAS in math, C evaluates operators in a fixed order when an expression has multiple operators.

### Order (highest to lowest priority)

| Priority    | Operators        | Associativity |
| ----------- | ---------------- | ------------- |
| 1 (highest) | `()` parentheses | left to right |
| 2           | `*`, `/`, `%`    | left to right |
| 3 (lowest)  | `+`, `-`         | left to right |

**Associativity** = when two operators share the same priority, which one is evaluated first (here, left-to-right).

### Worked Examples

```c
int result = 5 + 3 * 2;
```

`*` before `+`: `3 * 2 = 6`, then `5 + 6 = 11`. (Not `(5+3)*2 = 16`.)

```c
int result = 10 - 4 / 2;
```

`/` before `-`: `4 / 2 = 2`, then `10 - 2 = 8`.

```c
int result = 20 / 4 * 2;
```

Same priority → left to right: `20 / 4 = 5`, then `5 * 2 = 10`. (Not `20 / (4*2) = 2.5`.)

### Overriding with Parentheses

```c
int result = (5 + 3) * 2;   // parentheses first → 8 * 2 = 16
```

**Best practice:** use parentheses in complex expressions even when precedence rules are known — improves readability for others (or future you).

### Step-by-Step Example

```c
int x = 10 + 2 * 3 - 8 / 4;
```

1. `*` and `/` first (left to right): `2 * 3 = 6`, `8 / 4 = 2`
2. Now: `10 + 6 - 2`
3. `+` and `-` left to right: `10 + 6 = 16`, then `16 - 2 = 14`
4. `x = 14`

### Assignment Operators

| Operator | Meaning             | Equivalent             |
| -------- | ------------------- | ---------------------- |
| `+=`     | add and assign      | `a += 5` → `a = a + 5` |
| `-=`     | subtract and assign | `a -= 5` → `a = a - 5` |
| `*=`     | multiply and assign | `a *= 5` → `a = a * 5` |
| `/=`     | divide and assign   | `a /= 5` → `a = a / 5` |
| `%=`     | modulus and assign  | `a %= 5` → `a = a % 5` |

These have lower precedence than arithmetic operators — the right side is fully evaluated first, then assigned.