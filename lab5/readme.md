# Lab 5 Report

## Project Title
If-Else Statement Parser using Flex and Bison

## Project Overview
This lab implements a simple parser for `if` and `if-else` assignment statements using Flex and Bison. The parser validates a single statement per input line, checks the grammar, and reports whether the statement is valid.

## Objectives
- Design a grammar for `if` and `if-else` statements.
- Build a lexer to identify tokens such as `IF`, `ELSE`, `ID`, `RELOP`, `ASSIGN`, `NUM`, and `SEMICOLON`.
- Parse input statements and detect syntax errors.
- Provide user-friendly feedback for valid and invalid statements.

## Files in this Lab
- `ifelse.y` - Bison grammar file defining parser rules and error handling.
- `ifelse.l` - Flex lexer file defining token patterns and input scanning.
- `ifelse.tab.c` - Generated parser C source file from Bison.
- `ifelse.tab.h` - Generated header file from Bison.
- `lex.yy.c` - Generated lexer C source file from Flex.
- `ifelsechecker` - Compiled executable for the parser.

## Tools and Environment
- macOS
- Flex (Fast Lexical Analyzer)
- Bison (GNU parser generator)
- GCC / Clang C compiler
- Terminal or command-line shell

## Methodology
1. Define the lexical tokens in `ifelse.l`.
2. Define the parser grammar and precedence in `ifelse.y`.
3. Use Bison to generate `ifelse.tab.c` and `ifelse.tab.h`.
4. Use Flex to generate `lex.yy.c`.
5. Compile the generated sources with `gcc` or `clang`.
6. Run the parser and test with sample statements.

## Compilation Instructions
Run the following command in the `lab5` directory:

```bash
gcc ifelse.tab.c lex.yy.c -o ifelsechecker
```

## Execution Instructions
Run the parser executable:

```bash
./ifelsechecker
```

Then enter one statement per line.

## Sample Inputs
Valid examples:
- `if (a>b) x=y;`
- `if (a<=10) result=1;`
- `if (x!=y) total=num;`
- `if (a>b) x=y; else x=z;`
- `if (score==100) grade=A; else grade=B;`

Invalid examples:
- `if a>b x=y;` (missing parentheses)
- `if (a>b) x=y` (missing semicolon)
- `if (a>b) x=y; else` (missing second statement)

## Results
- The code parses valid `if` and `if-else` statements correctly.
- The parser prints `valid` when the input conforms to the grammar.
- Invalid syntax triggers a syntax error message: `Syntax Error: Invalid statement`.

## Discussion
- The parser supports identifiers, numeric literals, assignment statements, and comparison operators.
- The grammar uses precedence rules to handle the classic `dangling else` problem.
- The lexer terminates each parse invocation when a newline is encountered.

## Conclusion
The Lab 5 assignment is completed successfully. The parser correctly validates simple `if` and `if-else` assignment statements and reports syntax errors for incorrect input. This report documents the implementation, build process, and example usage.
