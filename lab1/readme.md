# Lab: Lexical Analyzer Using Flex (Keywords, Identifiers, Operators)

## Aim
To design and implement a lexical analyzer using **Flex** that identifies and classifies tokens such as:
- Keywords
- Identifiers
- Numbers
- Operators
- Separators
- Unknown symbols  
and displays them during scanning of input source code.

---

## Software Requirements
- Flex (Lexical Analyzer Generator)
- GCC Compiler
- Operating System: Windows / Linux / macOS

---

## Theory

A **lexical analyzer** is the first phase of a compiler. It reads input source code character by character and groups them into meaningful units called **tokens**.

In this program:
- Regular expressions define token patterns
- Flex matches input against these patterns
- Actions inside `{ }` execute when a pattern is matched
- Each token is printed immediately when detected

This helps in understanding:
- Token recognition
- Pattern matching using regular expressions
- Compiler front-end design

---

## Program Description

The program identifies the following tokens:

| Token Type   | Description |
|--------------|-------------|
| Keyword      | Reserved words like `int`, `float`, `if`, `else`, `return` |
| Identifier   | Variable/function names |
| Number       | Integer values |
| Operator     | Arithmetic and relational operators |
| Separator    | Symbols like `; , ( ) { }` |
| Unknown      | Any unrecognized symbol |

---

## Flex Program (tokenizer.l)

```lex
%{
#include <stdio.h>

int line_no = 1;
%}

DIGIT      [0-9]
ID         [a-zA-Z_][a-zA-Z0-9_]*
KEYWORD    (int|float|if|else|return)
OP         (==|!=|<=|>=|\+|\-|\*|\/|>|=)
SEPARATOR  [;,(){}]

%%

{KEYWORD}     { printf("Keyword: %s\n", yytext); }

{ID}          { printf("Identifier: %s\n", yytext); }

{DIGIT}+      { printf("Number: %s\n", yytext); }

{OP}          { printf("Operator: %s\n", yytext); }

{SEPARATOR}   { printf("Separator: %s\n", yytext); }

\n            { line_no++; }

[ \t]+        ;

.             { printf("Unknown symbol: %s\n", yytext); }

%%

int main() {
    printf("Enter code (Ctrl + D to end input):\n");
    yylex();
    return 0;
}

int yywrap() {
    return 1;
}