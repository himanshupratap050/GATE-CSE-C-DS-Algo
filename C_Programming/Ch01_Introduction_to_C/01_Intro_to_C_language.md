# Unit 1 — Introduction to C

> **Subject:** C Programming | **Level:** GATE CSE 2027 | **Language of notes:** Hinglish
> **Sources:** K&R (*The C Programming Language*, 2nd ed.), Kanetkar (*Let Us C*), Balagurusamy (*Programming in ANSI C*), Forouzan & Gilberg (*Computer Science: A Structured Programming Approach Using C*), ISO/IEC 9899 (C standard), D. Ritchie — *The Development of the C Language* (1993).
> Chapter numbers editions ke hisaab se badalte hain, isliye books ke references chapter/section level par diye hain.

## Contents

1. [Programming Languages — Basics](#1-programming-languages--basics)
2. [Algorithm & Flowchart](#2-algorithm--flowchart)
3. [History of C](#3-history-of-c)
4. [Definition & Characteristics of C](#4-definition--characteristics-of-c)
5. [Structure of a C Program](#5-structure-of-a-c-program)
6. [Compilation & Execution Process](#6-compilation--execution-process)
7. [Lexical Elements — Character Set, Tokens, Keywords, Identifiers](#7-lexical-elements)
8. [Kinds of Behaviour in C (Defined / Implementation-defined / Unspecified / Undefined)](#8-kinds-of-behaviour-in-c)
9. [Solved Trace Examples](#9-solved-trace-examples)
10. [GATE Exam Angle](#10-gate-exam-angle)
11. [Practice MCQs](#11-practice-mcqs)
12. [Quick Revision Sheet](#12-quick-revision-sheet)

---

## 1. Programming Languages — Basics

### 1.1 Levels of language

| Level | Example | Kaisa dikhta hai | Translator | Portable? | Speed |
|---|---|---|---|---|---|
| **Machine language** (1GL) | `10110000 01100001` | Binary 0/1 | Koi nahi (CPU directly execute karta hai) | No (CPU-specific) | Fastest |
| **Assembly language** (2GL) | `MOV AL, 61h` | Mnemonics | **Assembler** | No (CPU-specific) | Very fast |
| **High-level language** (3GL) | C, C++, Java, Python | English-like statements | **Compiler / Interpreter** | Yes (mostly) | Compiler ke baad fast |

- Ek aur taxonomy: 4GL = SQL jaise declarative languages; 5GL = logic/constraint based (Prolog).
- C ko aksar **middle-level language** kaha jaata hai (Schildt aur kai Indian textbooks): HLL ke constructs + hardware ke paas ka access (pointers, bit ops). K&R khud ye label formally nahi dete; unka point ye hai ki C "very high level" nahi hai aur kisi specific application area ke liye specialized nahi hai.

### 1.2 Translators

| Translator | Input → Output | Kaam |
|---|---|---|
| **Assembler** | Assembly → Machine code | 1-to-1 mapping of mnemonics |
| **Compiler** | Poora HLL program → Machine code (object code) | Poore program ko ek saath translate karta hai, errors ki list deta hai |
| **Interpreter** | HLL statement → execute (line by line) | Translate + execute simultaneously; object file nahi banti |

### 1.3 Compiler vs Interpreter

| Basis | Compiler | Interpreter |
|---|---|---|
| Translation unit | Poora program | Ek statement/line at a time |
| Output | Separate executable/object file | Koi permanent executable nahi |
| Execution speed | Fast (translation ek baar) | Slow (har baar re-translate) |
| Error reporting | Compile ke time saare syntax errors ek saath | Pehli error par ruk jaata hai |
| Memory | Object code ke liye extra memory | Kam memory |
| Example | C, C++ | Python (CPython bytecode interpreter), JavaScript, BASIC |

> **Note:** Java/Python "purely" ek category mein nahi aate (bytecode + VM/JIT). Exam mein yeh distinction "C = compiled language" tak hi kaafi hai.

### 1.4 Programming paradigm (short)

- **Procedural / Structured** — program = functions/procedures ka set, top-down design. **C yahin aata hai.**
- **Object-Oriented** — C++, Java. **Functional** — Haskell, Lisp.
- **Structured programming theorem (Böhm–Jacopini):** koi bhi computable function sirf 3 constructs se express ho sakta hai: **sequence, selection (if/switch), iteration (loops)**. `goto` ki zaroorat nahi (C mein hai phir bhi).

---

## 2. Algorithm & Flowchart

**Algorithm** = finite sequence of well-defined, unambiguous steps jo ek problem solve kare.

Horowitz–Sahni ke 5 criteria (Knuth ke bhi wahi):

| Criterion | Matlab |
|---|---|
| Input | Zero ya usse zyada externally supplied quantities |
| Output | Kam se kam ek quantity produce ho |
| Definiteness | Har instruction clear aur unambiguous |
| Finiteness | Har valid input par finite steps mein terminate ho |
| Effectiveness | Har step basic aur feasible (pen-paper se ho sake) |

> **Program vs Algorithm:** Program ko finite hona zaroori nahi (OS ka scheduler infinite loop mein chalta hai); algorithm ko finiteness satisfy karni hi padti hai.

**Flowchart symbols**

| Symbol | Shape | Use |
|---|---|---|
| Terminal | Oval | Start / Stop |
| Process | Rectangle | Computation / assignment |
| Decision | Diamond | Condition (Yes/No) |
| Input/Output | Parallelogram | `scanf` / `printf` |
| Connector | Small circle | Flow ko jodne ke liye |
| Flow line | Arrow | Direction of control |
| Predefined process | Rectangle with double side bars | Function call / subroutine |

**Pseudocode example** (largest of two numbers):

```
START
  READ a, b
  IF a > b THEN  PRINT a
  ELSE           PRINT b
STOP
```

---

## 3. History of C

### 3.1 Ancestry (timeline)

```
ALGOL 60 (1960)
    │   (international committee; block structure, recursion)
    ▼
CPL (1963)           — Cambridge + London Univ.; bahut bada/complex
    ▼
BCPL (1967)          — Martin Richards (Cambridge); CPL ka simplified, typeless version
    ▼
B (1970)             — Ken Thompson, Bell Labs; BCPL se; typeless; UNIX ke early version (PDP-7/PDP-11)
    ▼
C (1972)             — Dennis Ritchie, Bell Labs (Murray Hill, NJ); PDP-11; B mein data types add kiye
    ▼
UNIX kernel rewritten in C (1973)
    ▼
K&R C (1978)         — "The C Programming Language" 1st edition
    ▼
ANSI C / C89 (1989)  → ISO C90 (1990) → C99 → C11 → C17 → C23
```

Key points:
- **B typeless tha** (sirf machine word). PDP-11 ke aane par byte-addressing aur different sizes (char, int) ki zaroorat padi → Ritchie ne **types** add kiye → naya language **C** (naam: B ke baad next letter).
- **Creator:** Dennis M. Ritchie (Bell Labs, AT&T). Ken Thompson B ke creator hain aur UNIX ke bhi co-creator.
- C ki sabse badi early success: **UNIX OS ka kernel (assembly se) C mein rewrite** — isse OS-portability ka concept practical hua.
- **K&R book (1978)** ne 10 saal tak de-facto specification ka kaam kiya; isliye us era ki C ko **"K&R C"** ya *Traditional C* kehte hain.
- **Ritchie (1941–2011).**

### 3.2 Standardization

| Common name | Formal standard | Year | Note |
|---|---|---|---|
| K&R C | (koi formal standard nahi) | 1978 | Book hi specification thi |
| **C89 / ANSI C** | ANSI X3.159-1989 (X3J11 committee, formed 1983) | 1989 | Pehla official standard; function prototypes, `void`, `const`, `volatile` |
| **C90** | ISO/IEC 9899:1990 | 1990 | C89 ka ISO adoption, technically **same language** (sirf editorial changes) |
| C95 | Amendment 1 to C90 | 1995 | Wide-char support (`<wchar.h>`, `<wctype.h>`), digraphs, `<iso646.h>` |
| **C99** | ISO/IEC 9899:1999 | 1999 | `//` comments, `long long`, `_Bool`, `inline`, VLA, mixed declarations |
| **C11** | ISO/IEC 9899:2011 | 2011 | Threads, atomics, `_Generic`, `_Static_assert`, `gets()` removed |
| C17/C18 | ISO/IEC 9899:2018 | 2018 | Sirf bug-fix release, koi naya feature nahi |
| C23 | ISO/IEC 9899:2024 | 2024 | `bool/true/false/nullptr` keywords, `constexpr`, `typeof`, binary literals; trigraphs & K&R-style definitions removed |

> **Books mein terminology difference:**
> - Balagurusamy: *Traditional C (1972) → K&R C (1978) → ANSI C (1989) → ANSI/ISO C (1990) → C99*. Wo 1989 ko "ANSI C" aur 1990 ko "ANSI/ISO C" alag versions ki tarah dikhate hain, jabki language same hai.
> - K&R 2nd edition (1988) ANSI draft ko cover karti hai, isliye title page par "ANSI C" likha hota hai.
> - Kanetkar (older editions) Turbo C-based hain → `void main()`, `clrscr()`, `<conio.h>` jaise **non-standard** cheezein dikhti hain. GATE isse follow nahi karta.
> - GATE ke questions practically **ANSI C (C89/C90) + gcc-like behaviour** assume karte hain, C99 features kabhi-kabhi (jaise `//` comment, `for(int i...)`).

### 3.3 K&R C vs ANSI C

| Feature | K&R C | ANSI C |
|---|---|---|
| Function declaration | `int f();` (args unspecified) | Prototype: `int f(int, float);` |
| Function definition | `int f(a,b) int a; float b; { ... }` (old style) | `int f(int a, float b) { ... }` |
| `void`, `void *` | Nahi (`char *` generic pointer tha) | Hai |
| `const`, `volatile`, `signed` | Nahi | Hai |
| `enum` | Baad ke compilers mein | Standard |
| Standard library | Portable C library ad-hoc | Formally standardized (`<stdio.h>`, `<string.h>`, ...) |
| Preprocessor | Informal | `#`, `##`, `#elif`, `#error`, `#pragma` standardized |
| Structure assignment/passing | Shuruaati compilers mein nahi | Allowed |

### 3.4 C89 vs C99 vs C11 (GATE-relevant)

| Feature | C89 | C99 | C11 |
|---|---|---|---|
| `//` single-line comment | ✗ (extension) | ✓ | ✓ |
| Declarations mid-block | ✗ (block start par hi) | ✓ | ✓ |
| `for (int i=0; ...)` | ✗ | ✓ | ✓ |
| `long long`, `_Bool`, `_Complex` | ✗ | ✓ | ✓ |
| Implicit `int` (`main(){}`) | ✓ | ✗ (constraint violation) | ✗ |
| Implicit function declaration | ✓ | ✗ | ✗ |
| `return 0` implicit at end of `main` | ✗ | ✓ | ✓ |
| VLA (`int a[n];`) | ✗ | ✓ | Optional |
| `gets()` | ✓ | ✓ (deprecated) | **Removed** |
| Keywords count | 32 | 37 | 44 |

---

## 4. Definition & Characteristics of C

### 4.1 Definition

**C** ek **general-purpose, procedural (structured) programming language** hai jo Dennis Ritchie ne 1972 mein Bell Labs mein develop kiya. K&R ke words ka gist: C mein *economy of expression*, modern control flow, data structures aur rich operator set hai; ye chhota language hai, kisi ek application domain tak limited nahi.
*(Ref: K&R Preface & Introduction; Balagurusamy Ch. 1 "Overview of C"; Kanetkar Ch. 1.)*

### 4.2 Key characteristics

| Feature | Explanation |
|---|---|
| **Structured / Procedural** | Program functions mein divide hota hai; top-down design |
| **Portable** | Standard C ek machine se dusri machine par (recompile karke) chal jaata hai |
| **Efficient** | Chhota runtime, direct memory access; generated code fast |
| **Rich operator set** | Arithmetic, relational, logical, bitwise, assignment, `sizeof`, comma, ternary, etc. |
| **Small language** | 32 keywords (C89); I/O, string handling etc. **library** se, language ka part nahi |
| **Pointers & low-level access** | Direct address manipulation, hardware/OS programming ke liye |
| **Extensible via libraries** | Apne functions/header files banakar reuse |
| **Case-sensitive** | `Main` ≠ `main`, `INT` keyword nahi hai |
| **Free-form** | Whitespace/indentation meaning nahi rakhte (Python ke opposite) |
| **Weakly/statically typed** | Compile-time types; implicit conversions bahut hain |

### 4.3 Applications

OS kernels (UNIX, Linux, Windows ke parts), device drivers, embedded systems / microcontrollers, compilers & interpreters (gcc, CPython), DBMS engines, network stacks, game engines, real-time systems.

### 4.4 Limitations

- **No OOP** (classes, inheritance nahi), no namespaces, no exception handling, no generics (C11 `_Generic` limited).
- **No bounds checking** on arrays → buffer overflow (undefined behaviour).
- **Manual memory management** → leaks, dangling pointers.
- Weak type safety (implicit conversions, `void *` casts).
- Standard library mein built-in GUI/networking/threads-in-language nahi (C11 threads optional).

---

## 5. Structure of a C Program

### 5.1 Sections (Balagurusamy's model)

```
┌──────────────────────────────┐
│ 1. Documentation section     │  /* comments: name, author, purpose */
│ 2. Link section              │  #include <stdio.h>
│ 3. Definition section        │  #define PI 3.14159
│ 4. Global declaration section│  int count;   (global vars, function prototypes)
│ 5. main() function section   │  int main(void) { declarations; statements; }
│ 6. Subprogram section        │  user-defined functions
└──────────────────────────────┘
```

> **Terminology note:** ye 6-section classification **Balagurusamy** ki hai. K&R aur Kanetkar aisi formal sections list nahi dete; K&R sirf bolte hain ki program = functions aur variables ka collection, aur execution `main` se shuru hota hai. Exam mein "execution kahan se start hota hai?" → `main()`.

### 5.2 Hello World

```c
#include <stdio.h>          /* link section: printf ka declaration */

int main(void)              /* execution yahin se shuru */
{
    printf("Hello, World!\n");   /* library function call */
    return 0;                    /* status: success to OS */
}
```

Line-by-line:

| Line | Kaam |
|---|---|
| `#include <stdio.h>` | Preprocessor directive; `stdio.h` ki contents source mein paste. `printf` ka prototype yahin se aata hai |
| `int main(void)` | Program ka entry point. `int` return type = exit status |
| `{ ... }` | Function body / block |
| `printf(...)` | Standard output par likhta hai; `\n` = newline |
| `return 0;` | `0` (ya `EXIT_SUCCESS`) = success; non-zero = failure (`EXIT_FAILURE`) |
| `;` | Statement terminator (C mein *terminator*, Pascal ki tarah separator nahi) |

### 5.3 Valid forms of `main`

| Form | Status |
|---|---|
| `int main(void)` | Standard ✓ |
| `int main(int argc, char *argv[])` | Standard ✓ (command-line args) |
| `main()` | C89: valid (implicit `int`). C99+: invalid/warning; **GCC 14+ by default error** |
| `void main()` | **Non-standard** for hosted environment (implementation-defined at best). Turbo C accept karta hai, gcc warning deta hai |
| `int main()` | Practically chalta hai; C mein `()` ka matlab "args unspecified" hai (C23 mein `(void)` ke equal) |

**Important points (GATE traps):**
- `main` return na kare → C89 mein exit status **undefined**; C99+ mein `}` par pahunchna = `return 0` (**sirf `main` ke liye**).
- **C mein `main()` ko recursively call kar sakte ho** (legal); **C++ mein illegal**.
- `main` ka naam reserved nahi hai (keyword nahi), lekin program ka entry-point hai.

### 5.4 Comments

| Type | Syntax | Standard |
|---|---|---|
| Block | `/* ... */` | C89 |
| Line | `// ...` | C99 (C89 mein compiler extension) |

- **Nesting allowed nahi:** `/* a /* b */ c */` → comment pehle `*/` par khatam; `c */` syntax error.
- String ke andar `/* */` comment nahi hota: `printf("/* hi */");` poora print hoga.
- Translation phase 3 mein comment → **single space** se replace hota hai (isliye `a/**/b` = `a b`, do tokens; `#define` ke concatenation ke liye kaam nahi karta).

### 5.5 Printing return values (intro-level tricky facts)

| Function | Return value |
|---|---|
| `printf` | Number of **characters printed** (error par negative) |
| `scanf` | Number of items **successfully assigned** (`EOF` agar input failure pehle hi ho) |
| `puts` | Non-negative on success, `EOF` on error |

---

## 6. Compilation & Execution Process

### 6.1 Pipeline

```
 prog.c   (source)
    │
    ▼  [1] PREPROCESSOR (cpp)        #include expand, #define replace, comments hataye, conditional compilation
 prog.i   (expanded source)
    │
    ▼  [2] COMPILER (cc1)            lexical + syntax + semantic analysis, optimization, code generation
 prog.s   (assembly)
    │
    ▼  [3] ASSEMBLER (as)            assembly → machine code
 prog.o   (relocatable object file; .obj on Windows)
    │
    ▼  [4] LINKER (ld)               + other .o files + library code (libc) → resolve external symbols
 a.out    (executable; .exe on Windows)
    │
    ▼  [5] LOADER (OS)               executable ko RAM mein load, process create, control `main` ko
 RUN
```

### 6.2 gcc commands

| Command | Kya karta hai | Output |
|---|---|---|
| `gcc -E prog.c` | Sirf preprocess | stdout (`-o prog.i` se file) |
| `gcc -S prog.c` | Compile tak (assembly) | `prog.s` |
| `gcc -c prog.c` | Assemble tak (link nahi) | `prog.o` |
| `gcc prog.c` | Poora build | `a.out` |
| `gcc prog.c -o prog` | Poora build, custom name | `prog` |
| `gcc -std=c99 -Wall prog.c` | Standard select + warnings | — |
| `./a.out` | Run (Linux/macOS) | — |

### 6.3 Common file extensions

| Extension | Kya hai |
|---|---|
| `.c` | C source |
| `.h` | Header file |
| `.i` | Preprocessed output |
| `.s` / `.asm` | Assembly |
| `.o` / `.obj` | Object file |
| `.a` / `.lib` | Static library |
| `.so` / `.dll` | Shared (dynamic) library |
| `a.out` / `.exe` | Executable |

### 6.4 Static vs Dynamic linking

| Basis | Static | Dynamic |
|---|---|---|
| Library code | Executable ke andar copy | Runtime par load (`.so`/`.dll`) |
| Executable size | Bada | Chhota |
| Memory | Har program apni copy | Library shared across processes |
| Update | Re-link zaroori | Library replace karke ho jaata hai |

### 6.5 Translation phases (ISO C, 5.1.1.2)

1. Physical source chars → source character set; **trigraphs** replace (`??/` → `\`)
2. **Line splicing:** backslash-newline hata di jaati hai
3. **Tokenization** (preprocessing tokens) + **comments → space**
4. **Preprocessing:** directives execute, macros expand
5. Character/escape sequences → execution character set
6. **Adjacent string literals concatenate** (`"ab" "cd"` → `"abcd"`)
7. **Compilation** (syntax/semantic analysis, code gen)
8. **Linking**

### 6.6 Types of errors

| Error | Kab pakda jaata hai | Example |
|---|---|---|
| **Preprocessor error** | Phase 4 | `#include <abc.h>` — file not found |
| **Syntax error** | Compile time | `int x = 5` (missing `;`) |
| **Semantic error** | Compile time | Undeclared variable, type mismatch, `int *p = 5.5;` |
| **Linker error** | Link time | `undefined reference to 'foo'` (function declare hai, define nahi) |
| **Runtime error** | Execution | Segmentation fault, divide by zero |
| **Logical error** | Kabhi nahi (compiler nahi pakadta) | `if (a = 5)` jab `==` chahiye tha |

### 6.7 Runtime memory layout (forward reference — detail Storage Classes / Pointers chapters mein)

```
High address ┌───────────────────────┐
             │ Stack   (locals, call │  ↓ typically grows downward
             │         frames)       │
             │          ...          │
             │ Heap    (malloc)      │  ↑ typically grows upward
             ├───────────────────────┤
             │ BSS   (uninitialized  │
             │  globals/static → 0)  │
             │ Data  (initialized    │
             │  globals/static)      │
             │ Text  (code) + rodata │  (string literals yahin, read-only)
Low address  └───────────────────────┘
```
> Growth direction aur exact layout **standard mandate nahi karta** — implementation-dependent.

---

## 7. Lexical Elements

### 7.1 C character set

| Category | Members |
|---|---|
| Letters | `A–Z`, `a–z` |
| Digits | `0–9` |
| Special characters | `+ - * / % = < > ! & \| ^ ~ ? : ; , . ' " ( ) [ ] { } # \ _` (aur space) |
| White space | space, horizontal tab, vertical tab, newline, form feed |
| Escape sequences | `\n \t \\ \' \" \0 \a \b \r \f \v` |

Balagurusamy character set ko *letters, digits, special characters, white spaces* mein categorize karte hain, aur **trigraph** table bhi dete hain (`??=` → `#`, `??/` → `\`, `??'` → `^`, `??(` → `[`, `??)` → `]`, `??<` → `{`, `??>` → `}`, `??!` → `|`, `??-` → `~`). C23 mein trigraphs hata diye gaye.

### 7.2 Tokens

**Token** = program ka smallest meaningful (lexical) unit. Compiler ka lexical analyzer source ko tokens mein todta hai.

| K&R (App. A §A2) — 6 classes | ISO C (6.4) — 5 categories |
|---|---|
| identifiers | identifier |
| keywords | keyword |
| constants | constant |
| string literals | string-literal |
| operators | **punctuator** (operators + separators dono) |
| other separators | — |

> **Terminology difference:** K&R operators aur separators ko alag rakhte hain (6 classes); ISO standard dono ko **punctuators** kehta hai (5 categories). Balagurusamy: *keywords, identifiers, constants, strings, special symbols, operators* (6). Counting-questions mein practically har operator/punctuator = 1 token, isliye count same aata hai.

### 7.3 Keywords (32 in C89/C90)

Reserved words — inhe identifier ke roop mein use nahi kar sakte.

| Category | Keywords |
|---|---|
| Data types | `int` `char` `float` `double` `void` |
| Type modifiers | `short` `long` `signed` `unsigned` |
| Type qualifiers | `const` `volatile` |
| Storage class | `auto` `register` `static` `extern` |
| User-defined types | `struct` `union` `enum` `typedef` |
| Control flow | `if` `else` `switch` `case` `default` `for` `while` `do` `break` `continue` `goto` `return` |
| Operator | `sizeof` |

Count: 5 + 4 + 2 + 4 + 4 + 12 + 1 = **32** ✓

**Baad ke standards:**
- **C99 (+5 = 37):** `_Bool`, `_Complex`, `_Imaginary`, `inline`, `restrict`
- **C11 (+7 = 44):** `_Alignas`, `_Alignof`, `_Atomic`, `_Generic`, `_Noreturn`, `_Static_assert`, `_Thread_local`
- **C23:** `bool`, `true`, `false`, `nullptr`, `constexpr`, `typeof`, `alignas`, `alignof`, `static_assert`, `thread_local` etc. proper keywords ban gaye (GATE scope ke bahar).
- **Non-standard (Turbo C):** `near`, `far`, `huge`, `pascal`, `cdecl`, `interrupt` — Kanetkar ke purane editions mein dikhte hain; GATE mein 32 hi count hote hain.
- `main`, `printf`, `define`, `include`, `NULL` **keywords nahi** hain.

### 7.4 Identifiers

Variable, function, array, struct, label, macro ke naam.

**Rules (K&R §2.1, Balagurusamy Ch. 2):**
1. Letters, digits, underscore `_` se bane ho.
2. **Pehla character digit nahi** ho sakta.
3. **Keyword nahi** ho sakta.
4. **Case-sensitive:** `count`, `Count`, `COUNT` alag hain.
5. Space ya special characters (`- $ @ #` ...) allowed nahi (standard mein). `$` ko gcc extension ke roop mein accept karta hai.
6. **Length (significant characters):**

| Standard | Internal identifiers (local/macros) | External identifiers (linker-visible) |
|---|---|---|
| C89 | 31 | **6** (aur case-insensitive ho sakte hain) |
| C99+ | 63 | 31 |

7. **Reserved identifiers:** `_` + uppercase letter ya `__` (double underscore) se shuru hone wale names implementation ke liye reserved hain; file scope par `_` se shuru hone wale bhi.

| Identifier | Valid? | Reason |
|---|---|---|
| `_count` | ✓ | Underscore se start allowed (par library-reserved names se bachein) |
| `x1`, `x_1` | ✓ | — |
| `Total` | ✓ | `total` se alag |
| `1x` | ✗ | Digit se start |
| `x-1` | ✗ | `-` operator hai (3 tokens: `x`, `-`, `1`) |
| `my var` | ✗ | Space |
| `int`, `for` | ✗ | Keywords |
| `For`, `INT` | ✓ | Case-sensitive, keyword nahi |
| `$x` | ✗ (standard) | gcc extension mein chalta hai |

### 7.5 Constants, string literals (bas overview — detail Unit 2 mein)

| Type | Example |
|---|---|
| Integer | `10`, `012` (octal), `0x1A` (hex), `10L`, `10U` |
| Floating | `3.14`, `2.5e-3`, `3.14f` |
| Character | `'A'`, `'\n'` (type **`int`** in C, `char` in C++) |
| String literal | `"Hello"` (type `char[6]`, null-terminated) |

Adjacent strings concatenate: `"Hel" "lo"` ≡ `"Hello"`.

### 7.6 Operators & punctuators (quick list)

- Arithmetic `+ - * / %`, increment/decrement `++ --`
- Relational `< > <= >= == !=`, logical `&& || !`
- Bitwise `& | ^ ~ << >>`
- Assignment `= += -= *= /= %= &= |= ^= <<= >>=`
- Misc `sizeof`, `?:`, `,`, `.`, `->`, `*` (deref), `&` (address), `()`, `[]`
- Separators/punctuators: `; , { } ( ) [ ] # ...`

### 7.7 Maximal munch (longest match) rule

Lexer hamesha **sabse lamba possible token** banata hai, chahe usse parsing fail ho jaye.

| Source | Lexer ka tokenization | Result |
|---|---|---|
| `a+++b` | `a` `++` `+` `b` | `(a++) + b` ✓ |
| `a+++++b` | `a` `++` `++` `+` `b` | `(a++)++ + b` → **compile error** (`a++` lvalue nahi) |
| `x=y/*p` | `x` `=` `y` `/*`… | `/*` comment start ho jaata hai! (space do: `y / *p`) |
| `a---b` | `a` `--` `-` `b` | `(a--) - b` ✓ |
| `a - - b` | `a` `-` `-` `b` | `a - (-b)` ✓ |
| `x=-1;` | `x` `=` `-` `1` `;` | Aajkal ✓ (K&R C mein `=-` ek operator tha; ab nahi) |

### 7.8 Token counting — method + solved examples

**Method:** Har keyword, identifier, constant, string literal (poori string = 1 token), operator aur punctuator = **1 token**. Whitespace aur comments token nahi hain.

| Statement | Tokens | Count |
|---|---|---|
| `int x = 10;` | `int` `x` `=` `10` `;` | **5** |
| `a = b+++c;` | `a` `=` `b` `++` `+` `c` `;` | **7** |
| `printf("%d", a++);` | `printf` `(` `"%d"` `,` `a` `++` `)` `;` | **8** |
| `int main(){return 0;}` | `int` `main` `(` `)` `{` `return` `0` `;` `}` | **9** |
| `printf("i=%d, &i=%x", i, &i);` | `printf` `(` `"i=%d, &i=%x"` `,` `i` `,` `&` `i` `)` `;` | **10** |

> Last wala classic GATE PYQ hai: options mein `3, 26, 10, 21` the; **10** sahi. Trap: string ke andar ke `&`, `,`, `%d` alag tokens **nahi** hain — poori string 1 token.

---

## 8. Kinds of Behaviour in C

GATE mein bahut asar wala concept. ISO C §3.4 ke hisaab se:

| Behaviour | Definition | Example |
|---|---|---|
| **Well-defined** | Standard exactly batata hai output/effect | `printf("%d", 2+3);` → `5` |
| **Implementation-defined** | Standard multiple choices deta hai; **compiler ko document karna zaroori** | `sizeof(int)`, `char` signed hai ya unsigned, negative signed int ka right shift, `int` ka size/range |
| **Unspecified** | Multiple possibilities, **document karna zaroori nahi**, har baar alag ho sakta hai | Function arguments ke evaluation ka order: `f(a(), b())`; `x() + y()` mein pehle kaun |
| **Undefined (UB)** | Standard koi requirement nahi lagata — crash, garbage, "sahi" output, kuch bhi | Signed integer overflow, out-of-bounds array access, null pointer dereference, `i = i++ + ++i`, division by zero, modifying string literal |
| **Locale-specific** | Local conventions par depend | Currency symbol, decimal separator |

Exam angle:
- GATE options mein aksar aata hai: *"compiler dependent"*, *"undefined"*, ya *"error"*. Pehchano ki cheez implementation-defined hai (har compiler ka ek fixed behaviour) ya UB (koi guarantee nahi).
- **Dono ko confuse mat karo:** `sizeof(int)` implementation-defined (gcc/x86-64 par 4) — result deterministic hai; `int a[3]; a[5]` = UB — result kuch bhi.
- Agar question mein "Assume 32-bit machine / sizeof(int)=4" diya ho toh implementation-defined cheez ka answer nikalna valid hai.

---

## 9. Solved Trace Examples

### Example 1 — Nested `printf`

```c
#include <stdio.h>
int main(void)
{
    printf("%d", printf("%d", printf("Hi")));
    return 0;
}
```

**Trace:** Function call se pehle arguments evaluate hote hain → innermost pehle.

| Step | Call | Output (screen) | Return value |
|---|---|---|---|
| 1 | `printf("Hi")` | `Hi` | `2` (2 chars) |
| 2 | `printf("%d", 2)` | `2` | `1` (1 char) |
| 3 | `printf("%d", 1)` | `1` | `1` |

**Output:** `Hi21`

### Example 2 — `sizeof` operand evaluate nahi hota

```c
printf("%d", sizeof(printf("Hi")));
```

- `sizeof` ka operand (expression) **evaluate nahi hota**, sirf uska **type** dekha jaata hai (compile time).
- `printf` ka return type `int` → `sizeof(int)`.
- Inner `printf("Hi")` **run hi nahi hota**, "Hi" print nahi hoga.
- **Output:** `4` (jab `sizeof(int)==4`, implementation-defined).
- Pedantic note: `sizeof` ka type `size_t` hai; `%d` se print karna technically mismatch hai (sahi format `%zu`). GATE mein `%d` chalta hai.

### Example 3 — Comment trap (C89 vs C99)

```c
printf("%d", 8 //* c */ 2
);
```

| Standard | Tokenization | Result |
|---|---|---|
| C89 (no `//` comments) | `/* c */` comment; baaki `8 / 2` | `4` |
| C99+ | `//` se line ke end tak comment; `printf("%d", 8 );` | `8` |

Isliye "C99 vs C89" kabhi-kabhi output badalta hai.

### Example 4 — Maximal munch

```c
int a = 5, b = 3;
int c = a+++b;
printf("%d %d %d", c, a, b);
```

- Tokens: `a` `++` `+` `b` → `(a++) + b`
- `a++` ki value `5` (post-increment) → `c = 5 + 3 = 8`; phir `a = 6`.
- **Output:** `8 6 3`

### Example 5 — Unsequenced modification (UB)

```c
int i = 5;
i = i++ + 1;
```

`i++` aur assignment dono `i` ko modify karte hain, **unsequenced** → **undefined behaviour**. Koi bhi answer (6, 7, ...) valid maana ja sakta hai. Detail: Operators chapter (sequence points).

---

## 10. GATE Exam Angle

**High-frequency patterns (Unit 1 se):**
1. **Token counting** (printf/`a+++b`-type statements) — string = 1 token.
2. **Keyword vs identifier** — `main`, `printf`, `include` keywords nahi; `For`, `INT` valid identifiers.
3. **Nested `printf`** — return value = number of characters printed.
4. **Compilation phases** — kaunsi error kis stage par (linker error vs compile error; `#include` preprocessor).
5. **Behaviour classification** — undefined / unspecified / implementation-defined.
6. **`sizeof` operand not evaluated.**
7. **Maximal munch** — `+++`, `---`, `/*` cases.
8. **Statement-type "True/False"** — C compiled hai, C case-sensitive hai, `main` recursively callable hai (C mein).

**Common traps:**
- `void main()` ko "always valid" maan lena — standard mein non-portable.
- "C ek high-level language hai" vs "middle-level" — GATE MCQ mein context dekho; safe choice: C procedural, compiled, structured.
- Comments nest nahi hote.
- `'A'` ka type C mein **`int`** hai (`sizeof('A') == sizeof(int)`), C++ mein `char`.
- 32 keywords → C89; agar C99/C11 mention ho toh count badlega.
- String literal ke andar comment/token nahi banta.
- `=` vs `==` logical error compile hota hai; gcc `-Wall` warning deta hai.

**Undefined/implementation-defined summary:**
`sizeof(int)`, char signedness, right-shift negative: **implementation-defined**. Arg evaluation order: **unspecified**. `i = i++`, overflow, OOB access: **undefined**.

---

## 11. Practice MCQs

**Q1.** C language ka direct predecessor kaun tha?
(A) BCPL (B) B (C) ALGOL 60 (D) CPL

**Q2.** `printf("%d", a++);` mein kitne tokens hain?
(A) 6 (B) 7 (C) 8 (D) 9

**Q3.** Neeche di list mein kitne valid identifiers hain (strict ISO C, extensions nahi)?
`_x`, `x_1`, `1x`, `x-1`, `for`, `For`, `$x`
(A) 2 (B) 3 (C) 4 (D) 5

**Q4.** Output kya hai?
```c
printf("%d", printf("Hi"));
```
(A) `Hi` (B) `2` (C) `Hi2` (D) `2Hi`

**Q5.** `undefined reference to 'foo'` error kis stage par aata hai?
(A) Preprocessing (B) Compilation (C) Assembling (D) Linking

**Q6.** Output (C89 compiler par)?
```c
printf("%d", 8 //* c */ 2
);
```
(A) 8 (B) 4 (C) Compile error (D) 16

**Q7.** `int a=5,b=3; int c = a+++b;` ke baad `c` aur `a`?
(A) 8, 5 (B) 8, 6 (C) 9, 6 (D) Compile error

**Q8.** Kaunsa statement C ke liye **true** hai?
(A) `main` ko recursively call nahi kar sakte
(B) `main` keyword hai
(C) C case-sensitive hai
(D) `printf` keyword hai

**Q9.** `i = i++ + 1;` ka behaviour?
(A) Well-defined (B) Implementation-defined (C) Unspecified (D) Undefined

**Q10.** `printf("%d", sizeof(printf("Hi")));` (assume `sizeof(int)=4`)?
(A) `Hi2` (B) `Hi4` (C) `4` (D) `2`

<details>
<summary><b>Answers & Explanations (pehle khud try karo)</b></summary>

1. **(B) B** — C directly B se aaya (BCPL → B → C).
2. **(C) 8** — `printf ( "%d" , a ++ ) ;`
3. **(B) 3** — `_x`, `x_1`, `For` valid. `1x` (digit), `x-1` (operator), `for` (keyword) invalid; `$x` strict ISO mein invalid (gcc extension).
4. **(C) `Hi2`** — inner prints `Hi`, returns 2; outer prints `2`.
5. **(D) Linking** — declaration hai (compile pass), definition nahi (link fail).
6. **(B) 4** — C89 mein `//` comment nahi, `/* c */` comment hai → `8 / 2`.
7. **(B) 8, 6** — `(a++)+b` = 5+3 = 8; `a` = 6.
8. **(C)** — C case-sensitive hai. (A) galat, `main` recursively callable hai; (B), (D) `main`/`printf` keywords nahi.
9. **(D) Undefined** — `i` ko do baar unsequenced modify kar rahe hain.
10. **(C) `4`** — `sizeof` operand evaluate nahi karta; sirf type `int` ka size.
</details>

---

## 12. Quick Revision Sheet

- **C:** Dennis Ritchie, Bell Labs, **1972**; ancestor: **ALGOL 60 → CPL → BCPL → B → C**. UNIX kernel **1973** mein C mein.
- **K&R book:** 1978 (1st ed.), 1988 (2nd ed., ANSI draft).
- **Standards:** C89 (ANSI) → C90 (ISO) → C99 → C11 → C17 → C23.
- **Keywords:** 32 (C89), 37 (C99), 44 (C11).
- **Compilation:** Preprocess → Compile → Assemble → Link → Load.
- **Entry point:** `main()`; return `0` = success.
- **Token:** keyword, identifier, constant, string literal, operator, punctuator; string = 1 token; **maximal munch**.
- **Identifiers:** letters/digits/`_`, digit se start nahi, keyword nahi, case-sensitive.
- **Errors:** syntax/semantic → compile time; `undefined reference` → link time; segfault → runtime.
- **Behaviours:** implementation-defined (documented), unspecified (undocumented choice), undefined (anything).
- **`printf` returns** chars printed; **`sizeof`** operand evaluate nahi karta.

---

**Aage:** [➡️ Unit 2 — Data Types, Variables & Constants](./02-data-types-variables-constants.md)
**Wapas:** [⬅️ Repository README](../README.md)
