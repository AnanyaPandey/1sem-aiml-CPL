# Topic 2: Components of a Computer System

## 1. Introduction

- Before writing programs, it is important to understand the basic parts of a computer system.
- A computer system works together using **hardware** (physical parts) and **software** (programs).
- The main components we study here are: **Processor, Memory, Disk, Operating System, and Compiler**.

## 2. Processor (CPU)

- **CPU** stands for **Central Processing Unit**.
- It is called the "brain" of the computer.
- It performs all calculations and controls all operations.

### How CPU Works — The Fetch-Decode-Execute Cycle

1. **Fetch** – CPU gets (fetches) an instruction from memory.
2. **Decode** – CPU understands (decodes) what the instruction means.
3. **Execute** – CPU carries out (executes) the instruction.

- This cycle repeats continuously, very fast (millions/billions of times per second), until the program finishes.

## 3. Memory (RAM)

- **RAM** stands for **Random Access Memory**.
- It is the computer's **temporary/working memory**.
- When a program runs, it is loaded into RAM so the CPU can access it quickly.

### Key Features of RAM

- **Volatile**: Data is lost when the power is turned off.
- **Fast**: Much faster to access than a disk.
- **Temporary**: Used only while a program is running.

## 4. Disk (Secondary Storage)

- Disk (Hard Disk / SSD) is used for **permanent storage**.
- Programs and files are saved here even after the computer is switched off.

### Key Features of Disk

- **Non-volatile**: Data stays even without power.
- **Slower** than RAM.
- **Large storage capacity** compared to RAM.

### RAM vs Disk — Comparison Table

| Point                | RAM (Memory)                      | Disk (Storage)                  |
| -------------------- | --------------------------------- | ------------------------------- |
| Nature               | Volatile (temporary)              | Non-volatile (permanent)        |
| Speed                | Very fast                         | Slower                          |
| Use                  | Stores data/program while running | Stores data/program permanently |
| Size                 | Smaller capacity                  | Larger capacity                 |
| Data after power-off | Lost                              | Retained                        |

## 5. Where a Program is Stored and Executed

Understanding this step-by-step is very important:

1. You write a program and **save it on the disk** (as a file, e.g., `hello.c`).
2. When you run the program, it is **copied from disk into RAM**.
3. The **CPU fetches instructions from RAM**, not directly from disk (disk is too slow for the CPU to use directly).
4. The CPU executes the instructions one by one.
5. Once the program finishes, it is removed from RAM (but the file remains safely on disk).

**Simple flow:** `Disk (permanent storage) → RAM (temporary, while running) → CPU (executes instructions)`

## 6. Operating System (OS)

- The **Operating System** is special software that manages the entire computer system.
- Examples: Windows, Linux, macOS.

### Main Functions of an OS

- Manages hardware (CPU, memory, disk, input/output devices).
- Runs and manages programs (allocates memory, CPU time, etc.).
- Provides a way for users to interact with the computer (interface).
- Manages files and folders.
- Handles multiple programs running at the same time.

## 7. Compiler

- A **compiler** is a special program that translates **source code** (written by the programmer, in a high-level language like C) into **machine code** (0s and 1s) that the CPU can understand.

### Steps in Compilation (Simple View)

1. Programmer writes source code (e.g., `hello.c`).
2. Compiler checks the code for errors.
3. If no errors, compiler converts the code into machine code (creates an executable file).
4. This executable file can now be run by the CPU.

### Why Do We Need a Compiler?

- CPU understands only machine language (0s and 1s).
- Humans write in high-level language (C, easy to read).
- Compiler acts as a **translator** between the two.

## 8. Putting It All Together — How a Program Runs

1. Programmer writes C code and saves it on the **disk**.
2. The **compiler** translates the code into machine code.
3. The **operating system** loads the program from disk into **RAM**.
4. The **CPU** fetches instructions from RAM and executes them.
5. Output is shown to the user.

## 9. Quick Recap (One-Line Points)

- CPU = brain of the computer; follows Fetch → Decode → Execute cycle.
- RAM = temporary, fast, volatile memory used while a program runs.
- Disk = permanent, slower storage used to save files/programs.
- Program is stored on disk, loaded into RAM, and executed by CPU.
- OS = manages hardware, software, and resources of the computer.
- Compiler = converts high-level source code into machine code.