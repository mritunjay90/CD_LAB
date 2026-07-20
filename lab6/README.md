Lab 6 — FIRST and FOLLOW Sets Report
==================================

Overview
--------
This program computes FIRST and FOLLOW sets for a small CFG (converted arithmetic expression grammar).
The implementation lives in `lab6.cpp` and uses single-character nonterminals (E, X, T, Y, F) where E' and T' were converted to X and Y respectively.

Files
-----
- lab6.cpp — source that builds FIRST and FOLLOW sets and prints them.
- README.md — this report.

Build
-----
To compile (macOS / clang):

```bash
clang++ -std=c++17 lab6.cpp -o lab6
```

Run
---

```bash
./lab6
```

Sample Output
-------------
The program prints FIRST and FOLLOW sets. Example output (from a sample run):

------ FIRST SETS ------
FIRST(E) = { (, i }
FIRST(X) = { +, e }
FIRST(T) = { (, i }
FIRST(Y) = { *, e }
FIRST(F) = { (, i }

------ FOLLOW SETS ------
FOLLOW(E) = { $, ) }
FOLLOW(X) = { $, ) }
FOLLOW(T) = { +, $, ) }
FOLLOW(Y) = { +, $, ) }
FOLLOW(F) = { *, +, $, ) }

Notes
-----
- The code assumes nonterminals are single uppercase letters; multi-character heads like `E'` were converted to `X`/`Y` in the active grammar.
- Terminals: `i` is used for identifier (originally `id`), `e` denotes epsilon, and `$` denotes end-of-input.

Suggested next steps
--------------------
- If you want to support multi-character nonterminals (e.g., `E'`, `T'`), update the `GrammarRule` structure to store a string `head` instead of `char`, and adjust lookups accordingly.
- Add more test grammars and unit tests to validate corner cases (left recursion, longer productions).

If you want, I can now:
- change the code to support string nonterminals, or
- add more sample grammars and automated tests.
