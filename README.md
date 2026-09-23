# GATE CSE 2027 — C, Data Structures & Algorithms Notes

Exam-oriented, chapter-wise notes for **GATE CSE 2027** covering **C Programming, Data Structures and Algorithms**.
Prepared while following **Amit Khurana Sir's GATE CSE course**, and combined with theory from standard reference books.

> **Language:** English.
> **Status:** 🚧 Work in progress — chapters are added lecture by lecture.

---

## Table of Contents

1. [About this repo](#about-this-repo)
2. [GATE syllabus covered](#gate-syllabus-covered)
3. [Repository structure](#repository-structure)
4. [How every note file is organised](#how-every-note-file-is-organised)
5. [Reference books](#reference-books)
6. [Conventions used](#conventions-used)
7. [Progress tracker](#progress-tracker)
8. [How to use these notes](#how-to-use-these-notes)
9. [Feedback and corrections](#feedback-and-corrections)
10. [Disclaimer and license](#disclaimer-and-license)

---

## About this repo

- **Course followed:** Amit Khurana Sir — GATE CSE (the lecture order may differ slightly from the folder order below).
- **Goal:** for every topic, combine the lecture content, book-quality theory, solved GATE-style examples and practice questions.
- **Every file is self-contained** — any chapter can be read on its own.
- Wherever the lecture and the reference books use different terminology, the difference is marked explicitly with ⚠️.

---

## GATE syllabus covered

The relevant sections of the official GATE CS syllabus, on which this repo is built:

**Programming and Data Structures**
- Programming in C
- Recursion
- Arrays, stacks, queues, linked lists
- Trees, binary search trees, binary heaps
- Graphs

**Algorithms**
- Searching, sorting, hashing
- Asymptotic worst-case time and space complexity
- Algorithm design techniques: greedy, dynamic programming, divide-and-conquer
- Graph traversals, minimum spanning trees, shortest paths

> **Notes on scope:**
> - In the official syllabus, **hashing** is listed under Algorithms; this repo places it under **Data Structures**, following the course scope.
> - **AVL trees** are not named explicitly in the official syllabus text, but they appear in GATE previous-year questions, so they are included.
> - This list is a summary. Always verify it against the official **GATE 2027 information brochure**.

### C Programming — detailed scope
Data types, variables and constants, operators and precedence, control flow, functions and recursion, storage classes, pointers, arrays, strings, structures and unions, dynamic memory, preprocessor, file handling, output prediction and tricky code.

---

## Repository structure

```
GATE-CSE-2027-C-DS-Algo/
│
├── README.md
├── LICENSE
│
├── Resources/
│   ├── Book_References.md            # chapter → book/section mapping
│   ├── Course_Lecture_Map.md         # lecture → notes file mapping
│   ├── Formula_Sheet.md              # complexity, recurrence, tree/heap/hashing formulas
│   ├── PYQ_Tracker.md                # previous-year questions, topic-wise
│   └── Error_Log.md                  # personal notebook of mistakes and traps
│
├── _assets/                          # diagrams / images used in the notes
│
├── C_Programming/
│   ├── Ch01_Introduction_to_C/
│   │   └── 01_Intro_to_C_Language.md                      ✅
│   ├── Ch02_Data_Types_Variables_Constants/
│   │   ├── 01_Structure_and_Tokens.md
│   │   ├── 02_Data_Types_and_Modifiers.md
│   │   ├── 03_Variables_Constants_Literals.md
│   │   └── 04_sizeof_and_Type_Conversion.md
│   ├── Ch03_Operators_and_Expressions/
│   │   ├── 01_Operator_Types.md
│   │   ├── 02_Precedence_and_Associativity.md
│   │   ├── 03_Side_Effects_and_Sequence_Points.md
│   │   └── 04_Bitwise_Operators.md
│   ├── Ch04_Input_Output/
│   │   ├── 01_printf_and_Format_Specifiers.md
│   │   └── 02_scanf_and_Buffering.md
│   ├── Ch05_Control_Flow/
│   │   ├── 01_if_else_and_switch.md
│   │   ├── 02_Loops.md
│   │   └── 03_break_continue_goto.md
│   ├── Ch06_Functions_and_Recursion/
│   │   ├── 01_Function_Basics.md
│   │   ├── 02_Parameter_Passing.md
│   │   ├── 03_Recursion_and_Stack_Trace.md
│   │   └── 04_Variable_Arguments.md
│   ├── Ch07_Storage_Classes_and_Scope/
│   │   ├── 01_auto_register_static_extern.md
│   │   └── 02_Scope_Lifetime_Linkage.md
│   ├── Ch08_Pointers/
│   │   ├── 01_Pointer_Basics.md
│   │   ├── 02_Pointer_Arithmetic.md
│   │   ├── 03_Pointers_and_Arrays.md
│   │   ├── 04_Pointer_to_Pointer_and_Function_Pointers.md
│   │   └── 05_const_void_and_Dangling_Pointers.md
│   ├── Ch09_Arrays/
│   │   ├── 01_One_Dimensional_Arrays.md
│   │   ├── 02_Multidimensional_Arrays.md
│   │   └── 03_Arrays_and_Functions.md
│   ├── Ch10_Strings/
│   │   ├── 01_Strings_and_String_Literals.md
│   │   └── 02_String_Library_Functions.md
│   ├── Ch11_Structures_Unions_Enums/
│   │   ├── 01_Structures.md
│   │   ├── 02_Unions.md
│   │   ├── 03_enum_typedef_Bitfields.md
│   │   └── 04_Padding_and_Alignment.md
│   ├── Ch12_Dynamic_Memory/
│   │   ├── 01_malloc_calloc_realloc_free.md
│   │   └── 02_Memory_Layout_and_Leaks.md
│   ├── Ch13_Preprocessor/
│   │   ├── 01_Macros_and_Include.md
│   │   └── 02_Conditional_Compilation.md
│   ├── Ch14_File_Handling/
│   │   └── 01_File_Operations.md
│   └── Ch15_Output_Prediction_and_Tricky_Code/
│       ├── 01_Undefined_and_Implementation_Defined_Behaviour.md
│       └── 02_Tricky_Snippets.md
│
├── Data_Structures/
│   ├── Ch01_Arrays_and_ADT/
│   │   ├── 01_ADT_and_Complexity_Basics.md
│   │   ├── 02_Array_Address_Calculation.md
│   │   └── 03_Sparse_and_Special_Matrices.md
│   ├── Ch02_Linked_Lists/
│   │   ├── 01_Singly_Linked_List.md
│   │   ├── 02_Doubly_and_Circular_Linked_List.md
│   │   └── 03_Linked_List_Tricky_Problems.md
│   ├── Ch03_Stack/
│   │   ├── 01_Stack_ADT_and_Implementation.md
│   │   ├── 02_Infix_Postfix_Prefix.md
│   │   └── 03_Stack_Applications_and_Permutations.md
│   ├── Ch04_Queue/
│   │   ├── 01_Queue_and_Circular_Queue.md
│   │   ├── 02_Deque_and_Priority_Queue.md
│   │   └── 03_Stack_Queue_Interconversion.md
│   ├── Ch05_Trees/
│   │   ├── 01_Tree_Terminology_and_Binary_Trees.md
│   │   ├── 02_Tree_Traversals.md
│   │   └── 03_Height_Nodes_Counting_Numericals.md
│   ├── Ch06_Binary_Search_Tree/
│   │   ├── 01_BST_Operations.md
│   │   └── 02_BST_Numericals.md
│   ├── Ch07_AVL_Trees/
│   │   ├── 01_Rotations_Insertion_Deletion.md
│   │   └── 02_AVL_Numericals.md
│   ├── Ch08_Heap/
│   │   ├── 01_Binary_Heap_and_Heapify.md
│   │   └── 02_Heap_Numericals.md
│   ├── Ch09_Hashing/
│   │   ├── 01_Hash_Functions_and_Collisions.md
│   │   ├── 02_Chaining_and_Open_Addressing.md
│   │   └── 03_Hashing_Numericals.md
│   └── Ch10_Graphs/
│       ├── 01_Graph_Terminology_and_Representation.md
│       └── 02_Graph_Properties_and_Counting.md
│
└── Algorithms/
    ├── Ch01_Asymptotic_Analysis/
    │   ├── 01_Asymptotic_Notations.md
    │   └── 02_Analysis_of_Loops_and_Functions.md
    ├── Ch02_Recurrences/
    │   ├── 01_Substitution_and_Recursion_Tree.md
    │   ├── 02_Master_Theorem.md
    │   └── 03_Recurrence_Numericals.md
    ├── Ch03_Searching/
    │   └── 01_Linear_and_Binary_Search.md
    ├── Ch04_Sorting/
    │   ├── 01_Elementary_Sorts.md
    │   ├── 02_Merge_Sort.md
    │   ├── 03_Quick_Sort.md
    │   ├── 04_Heap_Sort.md
    │   ├── 05_Linear_Time_Sorts_and_Lower_Bound.md
    │   └── 06_Sorting_Comparison_and_Numericals.md
    ├── Ch05_Divide_and_Conquer/
    │   ├── 01_Divide_and_Conquer_Framework.md
    │   └── 02_Classic_Problems.md
    ├── Ch06_Greedy_Method/
    │   ├── 01_Greedy_Framework.md
    │   └── 02_Huffman_Job_Sequencing_Knapsack.md
    ├── Ch07_Dynamic_Programming/
    │   ├── 01_DP_Framework.md
    │   ├── 02_Knapsack_LCS_LIS.md
    │   └── 03_Matrix_Chain_and_Other_Problems.md
    ├── Ch08_Graph_Traversals/
    │   ├── 01_BFS.md
    │   └── 02_DFS_and_Edge_Classification.md
    ├── Ch09_Minimum_Spanning_Tree/
    │   └── 01_Kruskal_Prim_and_Union_Find.md
    └── Ch10_Shortest_Paths/
        ├── 01_Dijkstra_and_Bellman_Ford.md
        └── 02_Floyd_Warshall_and_All_Pairs.md
```

**Naming rules**
- Folders: `ChNN_Topic_Name/` (chapter order = study order).
- Files: `NN_Topic_Name.md`.
- Each chapter folder will end with a `99_Practice_and_PYQ.md` file (chapter-wise practice and previous-year questions).
- `.pdf` versions are generated only on request (into a `pdf/` folder).

---

## How every note file is organised

Every topic file follows the same structure:

1. **Definition + key points** (with a book reference)
2. **Example** (real-world or code)
3. **Diagram** — text/table diagram, memory layout or stack trace, wherever useful
4. **Comparison table** (where relevant)
5. **🎯 GATE Exam Angle** — common traps, undefined / implementation-defined behaviour, high-frequency question patterns
6. **Practice questions** with answers

**Additional rules**
- **C code:** the output is always explained with a step-by-step trace (memory, pointers, precedence, `sizeof`), not just the final answer.
- **Data Structures / Algorithms:** **time and space complexity** are always stated, and numerical topics (recurrences, tree height/nodes, hashing collisions, sorting comparisons) include **solved GATE-style examples**.

**Legend used in the notes**

| Symbol | Meaning |
|---|---|
| 📒 | Point from the instructor's lecture |
| 📚 | Theory from a reference book |
| ⚠️ | Doubtful point / lecture-vs-book difference / common confusion |
| 🎯 | GATE exam angle |
| ✅ / 🚧 / ⬜ | Done / In progress / Not started |

---

## Reference books

| Subject | Books |
|---|---|
| **C Programming** | K&R — *The C Programming Language* (2nd ed.); E. Balagurusamy — *Programming in ANSI C*; Y. Kanetkar — *Let Us C*; Forouzan & Gilberg — *Computer Science: A Structured Approach Using C* |
| **Data Structures** | Forouzan & Gilberg; Horowitz & Sahni — *Fundamentals of Data Structures*; Tanenbaum — *Data Structures Using C* |
| **Algorithms** | CLRS — *Introduction to Algorithms*; Horowitz, Sahni & Rajasekaran — *Fundamentals of Computer Algorithms* |

Sentences in the notes are paraphrased (no exact passages are copied from the books). K&R section numbers are given at section level; chapter numbers of the other books vary between editions, so match them against your own copy.

---

## Conventions used

- **C standard:** C99 / gcc behaviour by default. Differences from C89 are noted where they matter.
- **Data sizes:** unless a question says otherwise, `int` = 4 bytes and a pointer = 8 bytes (64-bit) or 4 bytes (32-bit). Every example states its assumption. GATE questions usually specify this themselves.
- **Undefined vs unspecified vs implementation-defined:** these are three different things and are marked separately in the notes.
- **Complexity:** worst case by default; best and average cases are stated separately.
- **Indexing:** arrays are 0-based (as in C), unless an algorithm book requires 1-based (CLRS style — this will be noted).

---

## Progress tracker

### C Programming

| Ch | Chapter | Status |
|---|---|---|
| 01 | Introduction to C | ✅ |
| 02 | Data Types, Variables, Constants | ⬜ |
| 03 | Operators and Expressions | ⬜ |
| 04 | Input / Output | ⬜ |
| 05 | Control Flow | ⬜ |
| 06 | Functions and Recursion | ⬜ |
| 07 | Storage Classes and Scope | ⬜ |
| 08 | Pointers | ⬜ |
| 09 | Arrays | ⬜ |
| 10 | Strings | ⬜ |
| 11 | Structures, Unions, Enums | ⬜ |
| 12 | Dynamic Memory | ⬜ |
| 13 | Preprocessor | ⬜ |
| 14 | File Handling | ⬜ |
| 15 | Output Prediction and Tricky Code | ⬜ |

### Data Structures

| Ch | Chapter | Status |
|---|---|---|
| 01 | Arrays and ADT | ⬜ |
| 02 | Linked Lists | ⬜ |
| 03 | Stack | ⬜ |
| 04 | Queue | ⬜ |
| 05 | Trees | ⬜ |
| 06 | Binary Search Tree | ⬜ |
| 07 | AVL Trees | ⬜ |
| 08 | Heap | ⬜ |
| 09 | Hashing | ⬜ |
| 10 | Graphs | ⬜ |

### Algorithms

| Ch | Chapter | Status |
|---|---|---|
| 01 | Asymptotic Analysis | ⬜ |
| 02 | Recurrences | ⬜ |
| 03 | Searching | ⬜ |
| 04 | Sorting | ⬜ |
| 05 | Divide and Conquer | ⬜ |
| 06 | Greedy Method | ⬜ |
| 07 | Dynamic Programming | ⬜ |
| 08 | Graph Traversals | ⬜ |
| 09 | Minimum Spanning Tree | ⬜ |
| 10 | Shortest Paths | ⬜ |

---

## How to use these notes

1. **Watch the lecture**, then read that day's chapter file and run the code yourself.
2. **Trace by hand** — draw the memory/stack trace on paper before looking at the output.
3. **Revise the 🎯 GATE Exam Angle** sections — the traps are found there.
4. **At the end of each chapter**, solve the practice questions and PYQs, and record your mistakes in `Resources/Error_Log.md`.
5. **Every week**, do a quick revision from `Formula_Sheet.md`.

To compile and run (Linux/macOS):

```bash
gcc -std=c99 -Wall -Wextra -o prog prog.c && ./prog
```

---

## Feedback and corrections

If you find a mistake or a doubtful statement in any note, please open a **GitHub Issue** with the file name, the section and the correct answer. Corrections are welcome.

---

## Disclaimer and license

- These are **personal study notes**. They are not affiliated with any coaching institute or course provider, and they are not a substitute for the course.
- Course slides/screenshots and book passages are **not redistributed** here; all notes are original write-ups.
- The notes may contain mistakes — cross-check with the official syllabus and standard books before relying on them for the exam.
- **License:** [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) (non-commercial use, with attribution, shared under the same license).
