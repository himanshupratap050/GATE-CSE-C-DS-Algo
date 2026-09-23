# Unit 1 — Introduction to C

> **Subject:** C Programming | **Target:** GATE CSE 2027
> **Lecture source:** Amit Khurana sir — *Intro to C Language* Part 1 and Part 2 (slides).
> **Book sources:** K&R (*The C Programming Language*, 2nd ed.), Kanetkar (*Let Us C*), Balagurusamy (*Programming in ANSI C*), Forouzan & Gilberg (*Computer Science: A Structured Programming Approach Using C*), ISO/IEC 9899 (C standard), D. Ritchie — *The Development of the C Language* (1993).
> Book chapter numbers vary by edition, so references are given at book/section level only.

**How to read this file:**
Parts 1–2 follow the lecture slides in order (every slide topic is covered). Part 3 adds book-level theory (history, program structure, tokens, behaviours) and GATE practice.
Blocks marked **Lecture note** point out where the lecture simplifies something or differs from the standard/books.

## Contents

**Part 1 — Background (lecture Part 1)**
1. [Program and Programming Language](#1-program-and-programming-language)
2. [Software: Application vs System](#2-software-application-vs-system)
3. [Types of Languages (LLL, HLL, 4GL, 5GL)](#3-types-of-languages)
4. [Language Translators: Assembler, Compiler, Interpreter](#4-language-translators)
5. [Where C Fits: Middle-Level Language](#5-where-c-fits-middle-level-language)

**Part 2 — C Basics (lecture Part 2)**
6. [Two Basic Components of Every Programming Language](#6-two-basic-components-of-every-programming-language)
7. [Advantages of C](#7-advantages-of-c)
8. [Types of Errors](#8-types-of-errors)
9. [Compilation Steps, Linker, Loader, Files Created](#9-compilation-steps-linker-loader-files-created)
10. [Keywords](#10-keywords)

**Part 3 — Book Theory and GATE Practice**
11. [History of C and Standards](#11-history-of-c-and-standards)
12. [Structure of a C Program](#12-structure-of-a-c-program)
13. [Identifiers, Tokens, Maximal Munch](#13-identifiers-tokens-maximal-munch)
14. [Kinds of Behaviour in C](#14-kinds-of-behaviour-in-c)
15. [Solved Trace Examples](#15-solved-trace-examples)
16. [GATE Exam Angle](#16-gate-exam-angle)
17. [Practice MCQs](#17-practice-mcqs)
18. [Quick Revision Sheet](#18-quick-revision-sheet)

---

# PART 1 — Background

## 1. Program and Programming Language

**Instruction:** a single command given to the computer, e.g. `z = x + y;`

**Program:** a *collection* of instructions, logically grouped, written in a programming language to perform a specific task.

> **Why "collection" and not "set"?** A *set* contains only unique elements. A program may contain the same instruction more than once, e.g.
> ```c
> z = x + y;
> z = x + y;      /* repeated instruction: allowed in a program */
> ```
> So a program is a **collection (sequence)** of instructions, not a set. This is the point the lecture stresses.

**Programming language:** a formal notation, defined by its **syntax** (grammar rules) and **semantics** (meaning), used to write programs. **C is a programming language.**

---

## 2. Software: Application vs System

**Software:** a collection of programs.

| Basis | Application Software | System Software |
|---|---|---|
| Purpose | Built according to a user's need/utility | Needed for the computer to function properly; manages hardware and provides a platform for other software |
| Dependency | Computer works without any particular application | Computer cannot function properly without system software |
| Examples | Games, antivirus, MS Office | Operating system, linker, loader (also compiler, assembler) |

**C can be used to build both** application software and system software (this is why C is called a powerful language; e.g. the UNIX operating system is written in C).

---

## 3. Types of Languages

```
                    Types of Languages
        ┌───────────┬───────────┬───────────┐
       LLL         HLL         4GL         5GL
   (Low Level)
    ┌───┴────┐
 Machine   Assembly
 language  language
```

| Type | Also called | Nature | Examples | Interface | Translator needed |
|---|---|---|---|---|---|
| Machine language | 1GL, binary language | 0s and 1s | Binary opcodes | — | None |
| Assembly language | 2GL | Mnemonics (ADD, SUB, MUL) | `MOV R0, 2000` | — | **Assembler** |
| High-level language (HLL) | 3GL | English-like | BASIC, COBOL, FORTRAN, C++, Java | **CUI** (Character/Command UI) | Compiler / Interpreter |
| 4GL | — | Minimum input, maximum output | VB, SQL | **GUI** | Yes |
| 5GL | — | Languages for A.I. | LISP, PROLOG | **VUI** (Voice UI) | Yes |

> **Lecture note:** the "generation" classification is a teaching classification, not defined in any ISO standard; different books draw the boundaries differently (e.g. many books treat VB as a 3GL/RAD tool). For GATE and the lecture, use the table above.

### 3.1 Machine language (binary language)

- **Definition:** the language of **0s and 1s**.
  - `0` = **absence of current** (low voltage, e.g. 0 V)
  - `1` = **presence of current** (high voltage, e.g. 5 V)
- A computer is an electronic device, so it can understand **binary language only**. This is the only language the CPU executes directly.
- **Advantage:** directly understood by the computer (no translation needed, fastest).
- **Disadvantages:**
  1. Difficult to learn, test and debug.
  2. **Machine dependent** (each CPU family has its own instruction set).

> **Lecture note:** 0 V / 5 V is the classic TTL representation; modern hardware uses other voltage levels (3.3 V, 1.8 V, ...). The logic-level idea is what matters.

### 3.2 Assembly language

- **Definition:** a low-level language in which **mnemonics** (short English-like symbols such as `ADD`, `SUB`, `MUL`) replace binary opcodes.
- In the lecture's simplified view, the operands are still given in binary, e.g. `10 ADD 101`.
- **Disadvantages:**
  1. Difficult to learn, test and debug.
  2. Mnemonics are **not understood by the computer**, so a language translator called an **Assembler** is required.
  3. Machine dependent (also true, though not written on the slide).

```
Assembly language program ──► [ Assembler ] ──► Machine language program
```

> **Lecture note:** in real assemblers, operands are registers, labels or immediate values written in decimal/hex (e.g. `MOV R0, 2000`), not necessarily binary. The slide's `10 ADD 101` is a simplification.

### 3.3 High-level language (HLL)

- **Definition:** English-like languages, hence **easily understood by the user (programmer)**.
- **Examples (as on the slide, now largely outdated):**
  - **BASIC** — Beginner's All-purpose Symbolic Instruction Code
  - **COBOL** — Common Business Oriented Language
  - **FORTRAN** — Formula Translation
  - Modern examples: C++, Java, Python.
- **Advantages:**
  1. Easily understood by the user.
  2. Easy to learn, test and debug.
  3. **Machine independent.**
- **Disadvantages:**
  1. **Cannot be understood by the computer**, so a **language translator** is needed.
  2. Because of this translation step, HLL programs are **less efficient** (than machine/assembly programs).
- An HLL uses **two types of language translators: Compiler and Interpreter.**

### 3.4 Fourth-generation language (4GL)

- **Definition:** languages designed for **minimum input and maximum output**; the programmer specifies *what* result is needed, not the detailed *how* (largely non-procedural/declarative).
- **Examples:** VB (Visual Basic), SQL.
- **Advantage:** a lot of development time is saved when building applications.
- **Disadvantages:**
  1. Needs more memory.
  2. Less efficient than HLL.

### 3.5 Fifth-generation language (5GL)

- **Definition:** languages meant for **Artificial Intelligence (A.I.)**.
- **Examples:** **LISP** and **PROLOG**.

> **Lecture note (name correction):** the slide expands LISP as "List Programming"; the standard expansion is **LISt Processing**. PROLOG = **PRO**gramming in **LOG**ic. If asked, use the standard expansions.

### 3.6 User-interface mapping

| Language level | Typical interface |
|---|---|
| HLL | **CUI** — Character User Interface (command line) |
| 4GL | **GUI** — Graphical User Interface |
| 5GL | **VUI** — Voice User Interface |

### 3.7 Comparison of all levels

| Basis | Machine | Assembly | HLL | 4GL | 5GL |
|---|---|---|---|---|---|
| Written with | 0/1 | Mnemonics | English-like | Near-natural, very short | A.I. constructs |
| Translator | None | Assembler | Compiler/Interpreter | Yes | Yes |
| Machine dependent | Yes | Yes | No | No | No |
| Ease of learning | Hardest | Hard | Easy | Easier | — |
| Execution efficiency | Highest | High | Medium | Lower than HLL | — |

---

## 4. Language Translators

A **language translator** converts a program written in one language into another (normally into machine language).

| Translator | Converts | Note |
|---|---|---|
| **Assembler** | Assembly → machine language | Used for assembly language |
| **Compiler** | HLL → machine language, **whole program at once** | e.g. C |
| **Interpreter** | HLL → machine language, **one statement at a time**, and executes it | e.g. classic BASIC, Python |

### 4.1 Compiler vs Interpreter (lecture table)

| # | Basis | Compiler | Interpreter |
|---|---|---|---|
| 1 | Translation | **As a whole** | **Line by line** |
| 2 | Debugging | Difficult | Easy |
| 3 | Speed | **Fast** | **Slow** |
| 4 | Output when the program has an error | **No output** (program is not produced/run) | Output is produced up to the line where the error occurs |
| 5 | RAM usage | Higher | Lower |

**Rules from the lecture:**
- A programming language **may use a compiler or an interpreter, but not both.**
- **Exception: Java and VB use both** a compiler and an interpreter.

> **Lecture note:** the first rule is a generalisation and the second is its exception. Java is compiled to bytecode by `javac` and then interpreted/JIT-compiled by the JVM. Python is likewise compiled to bytecode and then interpreted. **C is compiled.**

---

## 5. Where C Fits: Middle-Level Language

- C lies in **none of the four categories** above; it sits **between LLL and HLL**, hence it is called a **middle-level language**.
- It has features of **both**: **easy to understand like an HLL and powerful like an LLL**.

| Like HLL | Like LLL |
|---|---|
| English-like keywords, structured control flow, functions | Pointers and direct memory addresses, bitwise operators, register variables, close to hardware |

- **Inventor and year:** **Dennis Ritchie**, **1972**, **Bell Labs, USA**.
- C is **very powerful**: any kind of application can be built with it, e.g. virus, antivirus, games, text-editing software, **operating systems (e.g. UNIX)**.

> **Lecture note:** "middle-level" is a *descriptive label* (used by Schildt and many Indian textbooks); it is not in the ISO standard. K&R describe C as a general-purpose language that is **not** "very high level", and the ISO standard treats it as a general-purpose programming language. If a GATE/exam option offers "middle-level language", it is the intended answer.

---

# PART 2 — C Basics

## 6. Two Basic Components of Every Programming Language

1. **Language Translator** (compiler / interpreter / assembler)
2. **Library** — a **set of predefined functions** that come with the language.

- In C, `printf()` and `scanf()` are **library functions** (declared in `<stdio.h>`). The parentheses `( )` indicate a function call; the values inside are the arguments.
  ```c
  printf("Enter 2 no");     /* library function call with one argument (a string) */
  scanf("%d %d", &a, &b);   /* library function to read input */
  ```
- `printf` is **not** part of the C language grammar itself; it is provided by the **standard library**. (K&R Ch. 1 & App. B; Kanetkar Ch. on Input/Output.)

---

## 7. Advantages of C

| # | Advantage | Explanation |
|---|---|---|
| 1 | **Middle-level language** | Has features of both HLL (readability, structured code) and LLL (pointers, bit operations, hardware access) |
| 2 | **Portable** | The same source program can be compiled on different machines/operating systems with little or no change (a C compiler must exist for the target) |
| 3 | **Faster than other HLLs** | Compiles directly to native machine code; no virtual machine or garbage collector; minimal runtime overhead |
| 4 | **Rich in operators** | Arithmetic, relational, logical, bitwise, assignment, increment/decrement, conditional (`?:`), `sizeof`, comma, etc. |
| 5 | **Ability to extend its library** | Programmers can write their own functions and header files and add them to the library |

**Limitations (book-level, for completeness):**
- No object-oriented features, no namespaces, no built-in exception handling.
- **No array bounds checking** (out-of-bounds access is undefined behaviour).
- **Manual memory management** (leaks, dangling pointers).
- Weak type safety (many implicit conversions).

**Applications:** operating-system kernels (UNIX, Linux), device drivers, embedded systems, compilers/interpreters, database engines, network stacks, game engines.

---

## 8. Types of Errors

| # | Error | Definition | Detected by / when | Example |
|---|---|---|---|---|
| 1 | **Syntax error** | Violation of the grammar rules of the language | **Compiler**, at compile time; no object code is produced | Missing `;`, unmatched `{ }`, misspelt keyword |
| 2 | **Logical error** | Program compiles and runs, but the **logic is wrong**, so the output is wrong | **Not detected by the compiler**; found by testing/debugging | `avg = a + b / 2;` instead of `(a + b) / 2;`, `=` instead of `==` in a condition |
| 3 | **Runtime error** | Error that occurs **while the program is executing**, usually causing abnormal termination | At **run time** (OS/hardware signals) | Division by zero, segmentation fault (invalid memory access), file not found |

**Finer points (books/GATE):**
- **Semantic errors** (undeclared variable, type mismatch, wrong argument count) are also caught at compile time and are usually grouped under syntax errors in the 3-way classification.
- **Linker error**, e.g. `undefined reference to 'foo'` (function declared but never defined), is reported at **link time**. It is a build-time error, not a runtime error.
- **Preprocessor error**, e.g. `#include <abc.h>` — file not found, is reported in the preprocessing phase.

---

## 9. Compilation Steps, Linker, Loader, Files Created

### 9.1 Compilation steps (lecture view)

```
 Source code (.c)
        │
        ▼   compile
 Object code (.obj)   ← binary (machine code)
        │
        ▼   + Library     ── Linker ──►
 Executable file (.exe)
```

1. Write the **source code** (`.c`).
2. The **compiler** translates it into **object code** (`.obj`), which is **binary**.
3. The **linker** combines the object code with the **library** to produce the **executable file** (`.exe`).
4. The **loader** loads the `.exe` into RAM for execution.

### 9.2 Linker and Loader

| | Linker | Loader |
|---|---|---|
| Definition | A **system software** used to **link object code and library** to make an **executable file** | A **system software** used to **load the `.exe` file from hard disk (HD) into RAM** |
| Input | Object file(s) + library | Executable file |
| Output | Executable file | A running process in memory |
| Detail | Resolves external references (e.g. the address of `printf`) and combines multiple `.obj` files | Allocates memory, sets up the process and transfers control to the program's start-up code, which calls `main` |

Both linker and loader are **system software** (see Section 2).

### 9.3 Files created for each C program (lecture)

| # | File | Extension | Meaning |
|---|---|---|---|
| 1 | Source code | `.c` | Program written by the programmer |
| 2 | Object code | `.obj` | Binary output of the compiler |
| 3 | Executable file | `.exe` | Output of the linker; runs on the machine |
| 4 | Backup file | `.bak` | Backup copy of the previous version of the source file |

> **Lecture note:** this list describes the **Turbo C / DOS-Windows** environment. In a GCC/Linux environment the files are `.c`, `.o` (object) and `a.out` (executable), and **no `.bak` file is created**. In Turbo C, the `.bak` file is made by the IDE when you save a modified source file.

### 9.4 Detailed pipeline (book/GCC view)

The lecture shows 3 steps; a real C toolchain has these stages:

```
 prog.c ─► [1 Preprocessor] ─► prog.i ─► [2 Compiler] ─► prog.s ─► [3 Assembler] ─► prog.o ─► [4 Linker] ─► a.out ─► [5 Loader] ─► RUN
           #include, #define            syntax/semantic     assembly          machine code       + libc, other .o      (OS)
           comments removed             analysis, optimise                    (relocatable)
```

| GCC command | Effect | Output |
|---|---|---|
| `gcc -E prog.c` | Preprocess only | stdout |
| `gcc -S prog.c` | Up to assembly | `prog.s` |
| `gcc -c prog.c` | Up to object file (no linking) | `prog.o` |
| `gcc prog.c -o prog` | Full build | `prog` |
| `gcc -std=c99 -Wall prog.c` | Choose standard + enable warnings | — |

| Extension | Meaning |
|---|---|
| `.c` / `.h` | Source / header file |
| `.i` | Preprocessed source |
| `.s` | Assembly |
| `.o` / `.obj` | Object file |
| `.a` / `.lib` | Static library |
| `.so` / `.dll` | Shared (dynamic) library |
| `a.out` / `.exe` | Executable |

**Static vs dynamic linking**

| Basis | Static | Dynamic |
|---|---|---|
| Library code | Copied into the executable | Loaded at run time (`.so`/`.dll`) |
| Executable size | Larger | Smaller |
| Memory | Each program holds its own copy | Library shared between processes |
| Library update | Re-link needed | Replace the library only |

**Translation phases (ISO C, 5.1.1.2):**
1. Trigraph replacement (e.g. `??/` → `\`); 2. Line splicing (backslash-newline removed); 3. Tokenization, **comments → one space**; 4. **Preprocessing** (directives, macro expansion); 5. Escape sequences → execution character set; 6. **Adjacent string literals concatenated**; 7. **Compilation**; 8. **Linking**.

**Runtime memory layout (forward reference; detailed in Storage Classes / Pointers):**

```
High address ┌───────────────────────┐
             │ Stack (locals, frames)│  grows downward (typical)
             │          ...          │
             │ Heap (malloc)         │  grows upward (typical)
             ├───────────────────────┤
             │ BSS  (uninitialised   │
             │      globals/static)  │
             │ Data (initialised     │
             │      globals/static)  │
             │ Text (code) + rodata  │  string literals: read-only
Low address  └───────────────────────┘
```
Growth direction and exact layout are **not mandated** by the standard.

---

## 10. Keywords

**Definition:** **Reserved words** of a language that have a **specific meaning** to the compiler; the user **cannot use them for any other purpose** (e.g. as variable or function names).

- Examples: `int`, `char`, `float`, `if`, `switch`, `while`, `do`.
- **C has 32 keywords** (C89/C90).

### 10.1 The 32 keywords

| Category | Keywords |
|---|---|
| Data types | `int` `char` `float` `double` `void` |
| Type modifiers | `short` `long` `signed` `unsigned` |
| Type qualifiers | `const` `volatile` |
| Storage classes | `auto` `register` `static` `extern` |
| User-defined types | `struct` `union` `enum` `typedef` |
| Control flow | `if` `else` `switch` `case` `default` `for` `while` `do` `break` `continue` `goto` `return` |
| Operator | `sizeof` |

Count check: 5 + 4 + 2 + 4 + 4 + 12 + 1 = **32**.

### 10.2 "Any other purpose?" — what is and is not allowed

| Declaration | Valid? | Reason |
|---|---|---|
| `int n;` | ✓ | `n` is an ordinary identifier |
| `int if;` | ✗ | `if` is a keyword; cannot be used as a variable name |
| `int If;` | ✓ | C is **case-sensitive**: `If` ≠ `if`, and `If` is not a keyword |

- **C is a case-sensitive language:** `if` (keyword) ✓, `If` (not a keyword) — usable as an identifier. All 32 C keywords are written in **lower case**.

### 10.3 Later additions and non-standard keywords

| Standard | New keywords | Total |
|---|---|---|
| C89/C90 | — | **32** |
| C99 | `_Bool` `_Complex` `_Imaginary` `inline` `restrict` | 37 |
| C11 | `_Alignas` `_Alignof` `_Atomic` `_Generic` `_Noreturn` `_Static_assert` `_Thread_local` | 44 |
| C23 | `bool`, `true`, `false`, `nullptr`, `constexpr`, `typeof` etc. become proper keywords | (beyond GATE scope) |

- Turbo C adds non-standard keywords such as `near`, `far`, `huge`, `pascal`, `cdecl`, `interrupt`. GATE counts **32**.
- `main`, `printf`, `scanf`, `include`, `define`, `NULL` are **not keywords**.

---

# PART 3 — Book Theory and GATE Practice

## 11. History of C and Standards

### 11.1 Ancestry

```
ALGOL 60 (1960)
   ▼
CPL (1963)      Cambridge + London univ.; large and complex
   ▼
BCPL (1967)     Martin Richards; simplified, typeless CPL
   ▼
B (1970)        Ken Thompson, Bell Labs; typeless; early UNIX
   ▼
C (1972)        Dennis Ritchie, Bell Labs (Murray Hill, NJ); PDP-11; added data types
   ▼
UNIX kernel rewritten in C (1973)
   ▼
K&R C (1978) → ANSI C / C89 (1989) → ISO C90 → C99 → C11 → C17 → C23
```

- B was **typeless** (only the machine word). When the PDP-11 brought byte addressing and multiple data sizes, Ritchie added **types**, producing C (named as the successor to B).
- **Creator:** Dennis M. Ritchie (1941–2011). Ken Thompson created B and co-created UNIX.
- The **first UNIX was written in assembly**; by 1973 the kernel was rewritten in C, which established C as a system-programming language and showed OS portability.
- The **K&R book (1978)** served as the de-facto specification for a decade, so pre-ANSI C is called **K&R C** or *Traditional C*.

### 11.2 Standardisation

| Common name | Formal standard | Year | Notes |
|---|---|---|---|
| K&R C | none (the book) | 1978 | |
| **C89 / ANSI C** | ANSI X3.159-1989 (committee X3J11, formed 1983) | 1989 | First official standard; prototypes, `void`, `const`, `volatile` |
| **C90** | ISO/IEC 9899:1990 | 1990 | ISO adoption of C89; **same language**, editorial changes only |
| C95 | Amendment 1 to C90 | 1995 | Wide characters, digraphs |
| **C99** | ISO/IEC 9899:1999 | 1999 | `//` comments, `long long`, `_Bool`, `inline`, VLA, mixed declarations |
| **C11** | ISO/IEC 9899:2011 | 2011 | Threads, atomics, `_Generic`, `_Static_assert`; `gets()` removed |
| C17/C18 | ISO/IEC 9899:2018 | 2018 | Bug-fix release only |
| C23 | ISO/IEC 9899:2024 | 2024 | `bool/true/false/nullptr` keywords, `constexpr`, `typeof`; trigraphs removed |

> **Terminology differences between books:**
> - Balagurusamy lists *Traditional C (1972) → K&R C (1978) → ANSI C (1989) → ANSI/ISO C (1990) → C99*, presenting 1989 and 1990 as separate versions although the language is the same.
> - K&R 2nd edition (1988) covers the ANSI draft, so it is labelled "ANSI C".
> - Older Kanetkar editions are Turbo C based (`void main()`, `clrscr()`, `<conio.h>`), which are **non-standard**. GATE follows ANSI C with gcc-like behaviour.

### 11.3 K&R C vs ANSI C

| Feature | K&R C | ANSI C |
|---|---|---|
| Function declaration | `int f();` (arguments unspecified) | Prototype `int f(int, float);` |
| Function definition | `int f(a,b) int a; float b; {...}` | `int f(int a, float b) {...}` |
| `void`, `void *` | Absent (`char *` was the generic pointer) | Present |
| `const`, `volatile`, `signed` | Absent | Present |
| Standard library | Informal | Formally standardised |
| Structure assignment/passing | Missing in early compilers | Allowed |

### 11.4 C89 vs C99 vs C11

| Feature | C89 | C99 | C11 |
|---|---|---|---|
| `//` comments | ✗ (extension) | ✓ | ✓ |
| Declarations after statements | ✗ | ✓ | ✓ |
| `for (int i=0;...)` | ✗ | ✓ | ✓ |
| `long long`, `_Bool` | ✗ | ✓ | ✓ |
| Implicit `int` (`main(){}`) | ✓ | ✗ | ✗ |
| Implicit function declaration | ✓ | ✗ | ✗ |
| Implicit `return 0` at end of `main` | ✗ | ✓ | ✓ |
| VLA | ✗ | ✓ | Optional |
| Keywords | 32 | 37 | 44 |

---

## 12. Structure of a C Program

### 12.1 Sections (Balagurusamy)

```
┌──────────────────────────────┐
│ 1. Documentation section     │  /* comments */
│ 2. Link section              │  #include <stdio.h>
│ 3. Definition section        │  #define PI 3.14159
│ 4. Global declaration section│  global variables, function prototypes
│ 5. main() function section   │  int main(void) { ... }
│ 6. Subprogram section        │  user-defined functions
└──────────────────────────────┘
```

> **Terminology note:** the six-section model is Balagurusamy's. K&R and Kanetkar do not define such a list; K&R say a program is a set of functions and variables, and execution begins at `main`.

### 12.2 Hello World

```c
#include <stdio.h>          /* preprocessor directive: brings in printf's declaration */

int main(void)              /* execution starts here */
{
    printf("Hello, World!\n");
    return 0;               /* exit status: 0 = success */
}
```

| Element | Meaning |
|---|---|
| `#include <stdio.h>` | Preprocessor directive; copies the header into the source |
| `int main(void)` | Program entry point; `int` return value is the exit status |
| `{ }` | Function body (block) |
| `printf(...)` | Library function; writes to standard output |
| `return 0;` | `0` / `EXIT_SUCCESS` = success; non-zero = failure |
| `;` | Statement terminator |

### 12.3 Valid forms of `main`

| Form | Status |
|---|---|
| `int main(void)` | Standard ✓ |
| `int main(int argc, char *argv[])` | Standard ✓ |
| `main()` | Valid in C89 (implicit `int`); invalid in C99+ (GCC 14+ errors by default) |
| `void main()` | **Non-standard** for hosted environments; accepted by Turbo C, warned by gcc |
| `int main()` | Works; in C89–C17 empty `()` means "arguments unspecified" |

- If `main` reaches `}` without `return`: C89 → exit status undefined; C99+ → equivalent to `return 0` (**only for `main`**).
- **`main` can be called recursively in C** (legal); it is illegal in C++.

### 12.4 Comments

| Type | Syntax | Standard |
|---|---|---|
| Block | `/* ... */` | C89 |
| Line | `// ...` | C99 |

- Comments **do not nest**: `/* a /* b */ c */` ends at the first `*/`, and `c */` is a syntax error.
- Inside a string literal, `/* */` is not a comment: `printf("/* hi */");` prints it literally.
- A comment is replaced by **one space** (translation phase 3).

### 12.5 Return values of common library functions

| Function | Returns |
|---|---|
| `printf` | Number of **characters printed** (negative on error) |
| `scanf` | Number of items **successfully assigned** (`EOF` on input failure before the first conversion) |
| `puts` | Non-negative on success, `EOF` on error |

---

## 13. Identifiers, Tokens, Maximal Munch

### 13.1 Identifier rules (K&R §2.1; Balagurusamy Ch. 2)

An **identifier** is the name given to a variable, function, array, structure, label or macro.

1. Made of **letters, digits and underscore** only.
2. **First character cannot be a digit.**
3. **Cannot be a keyword.**
4. **Case-sensitive** (`count`, `Count`, `COUNT` are different).
5. No spaces or special characters (`$` is accepted by gcc only as an extension).
6. **Significant length:**

| Standard | Internal identifiers | External identifiers |
|---|---|---|
| C89 | 31 chars | **6 chars** (may be case-insensitive) |
| C99+ | 63 chars | 31 chars |

7. Identifiers beginning with `_` + uppercase letter, or with `__`, are **reserved** for the implementation.

| Identifier | Valid? | Reason |
|---|---|---|
| `_count`, `x_1`, `Total` | ✓ | — |
| `1x` | ✗ | Starts with digit |
| `x-1` | ✗ | `-` is an operator (three tokens) |
| `my var` | ✗ | Contains a space |
| `int`, `for` | ✗ | Keywords |
| `For`, `INT` | ✓ | Case-sensitive, not keywords |

### 13.2 Tokens

**Token:** the smallest meaningful lexical unit of a program.

| K&R (App. A §A2): 6 classes | ISO C (6.4): 5 categories |
|---|---|
| identifiers | identifier |
| keywords | keyword |
| constants | constant |
| string literals | string-literal |
| operators | **punctuator** (operators and separators together) |
| other separators | — |

> **Terminology difference:** K&R keep operators and separators apart (6 classes); ISO merges them as *punctuators* (5 categories). Balagurusamy lists keywords, identifiers, constants, strings, special symbols and operators. For counting questions, each operator/punctuator is one token in every scheme, so the count is the same.

### 13.3 Maximal munch (longest-match) rule

The lexer always forms the **longest possible token**, even if parsing then fails.

| Source | Tokens | Result |
|---|---|---|
| `a+++b` | `a` `++` `+` `b` | `(a++) + b` ✓ |
| `a+++++b` | `a` `++` `++` `+` `b` | `(a++)++ + b` → **compile error** (`a++` is not an lvalue) |
| `a---b` | `a` `--` `-` `b` | `(a--) - b` ✓ |
| `x=y/*p` | `x` `=` `y` `/*`... | `/*` starts a comment! Write `y / *p` |

### 13.4 Counting tokens

**Method:** each keyword, identifier, constant, operator and punctuator = 1 token; **a whole string literal = 1 token**; whitespace and comments are not tokens.

| Statement | Tokens | Count |
|---|---|---|
| `int x = 10;` | `int` `x` `=` `10` `;` | **5** |
| `a = b+++c;` | `a` `=` `b` `++` `+` `c` `;` | **7** |
| `printf("%d", a++);` | `printf` `(` `"%d"` `,` `a` `++` `)` `;` | **8** |
| `int main(){return 0;}` | `int` `main` `(` `)` `{` `return` `0` `;` `}` | **9** |
| `printf("i=%d, &i=%x", i, &i);` | `printf` `(` `"i=%d, &i=%x"` `,` `i` `,` `&` `i` `)` `;` | **10** |

The last one is a classic GATE PYQ (options 3, 26, 10, 21; answer **10**). Trap: characters inside the string are **not** separate tokens.

---

## 14. Kinds of Behaviour in C

(ISO C §3.4)

| Behaviour | Definition | Examples |
|---|---|---|
| **Well-defined** | The standard fixes the result exactly | `printf("%d", 2+3);` → `5` |
| **Implementation-defined** | The standard allows several choices; the **compiler must document** its choice | `sizeof(int)`, signedness of plain `char`, right shift of a negative signed value |
| **Unspecified** | Several outcomes allowed; **no documentation required**; may differ each time | Order of evaluation of function arguments `f(a(), b())` |
| **Undefined (UB)** | The standard imposes **no requirement** at all: crash, garbage, or "correct" output | Signed overflow, out-of-bounds access, null dereference, `i = i++ + ++i`, division by zero, modifying a string literal |
| **Locale-specific** | Depends on local conventions | Decimal separator, currency symbol |

GATE angle:
- Options often read *"compiler dependent"*, *"undefined"* or *"error"*. Distinguish **implementation-defined** (deterministic for a given compiler, e.g. `sizeof(int)`) from **undefined** (no guarantee, e.g. `a[5]` on `int a[3]`).
- If the question states "assume `sizeof(int) = 4`", the implementation-defined part is fixed and you can compute the answer.

---

## 15. Solved Trace Examples

### Example 1 — Nested `printf`

```c
printf("%d", printf("%d", printf("Hi")));
```

Arguments are evaluated before the call, so the innermost call runs first.

| Step | Call | Printed | Returns |
|---|---|---|---|
| 1 | `printf("Hi")` | `Hi` | 2 |
| 2 | `printf("%d", 2)` | `2` | 1 |
| 3 | `printf("%d", 1)` | `1` | 1 |

**Output:** `Hi21`

### Example 2 — `sizeof` does not evaluate its operand

```c
printf("%d", sizeof(printf("Hi")));
```

- The operand of `sizeof` is **not evaluated**; only its type is used (compile time).
- `printf` returns `int` → `sizeof(int)`. The inner `printf` never runs, so "Hi" is not printed.
- **Output:** `4` (when `sizeof(int) == 4`; implementation-defined).
- Pedantic: `sizeof` yields `size_t`; the correct format is `%zu`. GATE accepts `%d`.

### Example 3 — Comment trap (C89 vs C99)

```c
printf("%d", 8 //* c */ 2
);
```

| Standard | Interpretation | Output |
|---|---|---|
| C89 | `8 / (comment) 2` → `8 / 2` | `4` |
| C99+ | `//` comments out the rest of the line → `printf("%d", 8 );` | `8` |

### Example 4 — Maximal munch

```c
int a = 5, b = 3;
int c = a+++b;
printf("%d %d %d", c, a, b);
```

Tokens: `a` `++` `+` `b` → `(a++) + b`. `a++` yields 5, so `c = 5 + 3 = 8`, then `a = 6`.
**Output:** `8 6 3`

### Example 5 — Unsequenced modification (UB)

```c
int i = 5;
i = i++ + 1;
```

`i++` and the assignment both modify `i` with no sequencing between them → **undefined behaviour**. (Details in the Operators chapter, sequence points.)

---

## 16. GATE Exam Angle

**High-frequency patterns from this unit**
1. **Token counting**; a string literal is one token.
2. **Keyword vs identifier**: `main`, `printf`, `include` are not keywords; `If`, `INT` are valid identifiers.
3. **Nested `printf`**: it returns the number of characters printed.
4. **Errors by stage**: syntax/semantic → compile time; `undefined reference` → link time; segmentation fault → run time; wrong output with no diagnostic → logical error.
5. **Behaviour classification**: undefined vs unspecified vs implementation-defined.
6. **`sizeof` operand is not evaluated.**
7. **Maximal munch** (`+++`, `---`, `/*`).
8. **True/False statements**: C is compiled; C is case-sensitive; `main` may call itself in C.
9. **Theory MCQs from the lecture**: linker vs loader; compiler vs interpreter; 4GL/5GL examples; which files are created; who invented C and when.

**Common traps**
- Treating `void main()` as always valid.
- Assuming C is a pure HLL when the option says "middle-level language" (follow the lecture/book wording of the question).
- Comments do not nest.
- `'A'` has type **`int`** in C (`sizeof('A') == sizeof(int)`), `char` in C++.
- The 32-keyword count applies to C89; C99 has 37, C11 has 44.
- Anything inside a string literal is never a separate token or a comment.
- Linker error ≠ compile error ≠ runtime error.

---

## 17. Practice MCQs

**Q1.** Which language is the direct predecessor of C?
(A) BCPL (B) B (C) ALGOL 60 (D) CPL

**Q2.** How many tokens does `printf("%d", a++);` contain?
(A) 6 (B) 7 (C) 8 (D) 9

**Q3.** How many of the following are valid identifiers in strict ISO C?
`_x`, `x_1`, `1x`, `x-1`, `for`, `For`, `$x`
(A) 2 (B) 3 (C) 4 (D) 5

**Q4.** What is the output?
```c
printf("%d", printf("Hi"));
```
(A) `Hi` (B) `2` (C) `Hi2` (D) `2Hi`

**Q5.** `undefined reference to 'foo'` is reported by the:
(A) Preprocessor (B) Compiler (C) Assembler (D) Linker

**Q6.** Which software loads the `.exe` file from hard disk into RAM?
(A) Compiler (B) Linker (C) Loader (D) Assembler

**Q7.** For `int a=5,b=3; int c = a+++b;` the values of `c` and `a` are:
(A) 8, 5 (B) 8, 6 (C) 9, 6 (D) compile error

**Q8.** Which statement is true?
(A) `main` cannot be called recursively in C
(B) `main` is a keyword
(C) C is case-sensitive
(D) `printf` is a keyword

**Q9.** The language interface associated with 4GL is:
(A) CUI (B) GUI (C) VUI (D) None

**Q10.** Which of the following is **not** a property of an interpreter as described in the lecture?
(A) Line-by-line translation (B) Easy debugging (C) Faster execution than a compiler (D) Lower RAM usage

**Q11.** A program differs from a set because:
(A) a program has no order
(B) a program may contain repeated instructions
(C) a set can contain functions
(D) a program can only contain unique instructions

**Q12.** `printf("%d", sizeof(printf("Hi")));` (assume `sizeof(int)=4`) prints:
(A) `Hi2` (B) `Hi4` (C) `4` (D) `2`

<details>
<summary><b>Answers and explanations (try first)</b></summary>

1. **(B) B** — BCPL → B → C.
2. **(C) 8** — `printf ( "%d" , a ++ ) ;`
3. **(B) 3** — `_x`, `x_1`, `For` are valid; `1x` (digit first), `x-1` (operator), `for` (keyword) are not; `$x` is invalid in strict ISO C (gcc extension).
4. **(C) `Hi2`** — inner call prints `Hi` and returns 2; outer prints `2`.
5. **(D) Linker** — declared (compile passes) but not defined (link fails).
6. **(C) Loader.**
7. **(B) 8, 6** — `(a++) + b` = 5 + 3; `a` becomes 6.
8. **(C)** — (A) is false (recursion on `main` is legal in C); `main` and `printf` are not keywords.
9. **(B) GUI** — HLL → CUI, 4GL → GUI, 5GL → VUI.
10. **(C)** — an interpreter is **slower** than a compiler.
11. **(B)** — a set holds unique elements; a program can repeat an instruction such as `z = x + y;`.
12. **(C) `4`** — `sizeof` does not evaluate its operand.
</details>

---

## 18. Quick Revision Sheet

- **Program** = collection (not set) of instructions; **software** = collection of programs; **application** vs **system** software (OS, linker, loader).
- **Language types:** LLL (machine, assembly) → HLL → 4GL → 5GL. Interfaces: CUI, GUI, VUI.
- **Machine language:** 0/1 (0 = no current, 1 = current); **assembly:** mnemonics + assembler; **HLL:** English-like, machine independent, needs compiler/interpreter.
- **Compiler:** whole program, fast, no output on error, more RAM. **Interpreter:** line by line, slow, easy debugging, less RAM. Java/VB use both.
- **C:** middle-level language; Dennis Ritchie; 1972; Bell Labs; UNIX in C (1973). Lineage: ALGOL 60 → CPL → BCPL → B → C.
- **Two components of every language:** translator + library. `printf`/`scanf` are library functions.
- **Advantages of C:** middle-level, portable, fast, rich operators, extensible library.
- **Errors:** syntax, logical, runtime (+ linker/preprocessor at build time).
- **Build:** `.c` → compile → `.obj` → linker (+ library) → `.exe` → loader → RAM. Turbo C also makes `.bak`.
- **Keywords:** reserved, 32 in C89, all lower case; C is case-sensitive (`If` is not `if`).
- **Behaviours:** implementation-defined (documented), unspecified (undocumented choice), undefined (anything).
- **`printf` returns** the number of characters printed; **`sizeof`** does not evaluate its operand.

---

**Next:** [➡️ Unit 2 — Data Types, Variables & Constants](./02-data-types-variables-constants.md)
**Back:** [⬅️ Repository README](../README.md)
