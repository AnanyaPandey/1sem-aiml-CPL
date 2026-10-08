### History of C Language

#### Background: the languages before C

| Year | Language | Created by                        | Note                                                         |
| ---- | -------- | --------------------------------- | ------------------------------------------------------------ |
| 1960 | ALGOL 60 | International committee           | First structured language, but not suited for system programming |
| 1963 | CPL      | Cambridge and London universities | Too large and complex                                        |
| 1967 | BCPL     | Martin Richards                   | Simplified version of CPL                                    |
| 1970 | B        | Ken Thompson (Bell Labs)          | Simplified BCPL, used for early UNIX                         |

#### Birth of C (1972)

- **Dennis Ritchie** created C at **Bell Labs** between 1969 and 1973.
- It was built on top of B, adding data types and other features that B lacked. So basically C was an upgraded version of B programming language.
- It was first developed on a **DEC PDP-11** computer.
- The goal was to write the **UNIX operating system** in a language other than assembly.
- In **1973**, the UNIX kernel was rewritten in C. This was a big step, because it showed that an operating system could be written in a high-level language and still be fast.

#### K&R C (1978)

- Brian Kernighan and Dennis Ritchie published the book **"The C Programming Language"**.
- It became the unofficial standard, known as **K&R C**.
- C spread quickly to many different machines.

#### Standardization

| Year | Standard         | Note                                                         |
| ---- | ---------------- | ------------------------------------------------------------ |
| 1989 | **ANSI C (C89)** | First official standard by ANSI. Also adopted by ISO in 1990 (C90) |
| 1999 | **C99**          | Added `//` comments, `bool` type (`stdbool.h`), declaring variables inside `for`, `long long` |
| 2011 | **C11**          | Added multithreading support and other features              |
| 2017 | **C17**          | Bug fixes to C11, no new features                            |
| 2024 | **C23**          | Latest standard, adds `bool`, `true`, `false` as built-in keywords and other improvements |

#### Why C became so popular

1. **Portable:** the same program can run on different machines with little change
2. **Fast:** close to hardware, produces efficient machine code
3. **Small and simple:** few keywords, easy to learn the basics
4. **UNIX and later Linux** were written in C, which pushed its use everywhere
5. **Base for other languages:** C++, Java, C#, and Python's main implementation are all influenced by or built using C

#### Why it is called "C"

It came after the language **B**. The next letter of the alphabet was used.

#### Quick one-line summary for exams

> C was developed by **Dennis Ritchie** at **Bell Labs** in **1972** to write the **UNIX** operating system, and was standardized by ANSI in **1989**.