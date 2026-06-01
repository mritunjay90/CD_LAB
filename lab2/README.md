# Lab 3: Token Counter for Identifiers, Keywords & Operators Using Flex

## Aim
To develop a lexical analyzer using Flex that scans input source code and:
- Identifies tokens such as keywords, identifiers, numbers, operators, strings, comments, and delimiters
- Counts the frequency of each token type

---

## Software Requirements

- Flex (Lexical Analyzer Generator)
- GCC Compiler
- Operating System: Windows / Linux / macOS

---

## Theory

A lexical analyzer is the first phase of a compiler. It reads the source code and converts it into meaningful tokens that are later used by the parser.

In this experiment:
- Regular expressions are used to define token patterns
- Flex matches input against these patterns
- Actions inside `{ }` are executed when a pattern is matched
- Counters are used to track frequency of each token type

This helps in understanding compiler design fundamentals such as:
- Token recognition
- Pattern matching
- Symbol classification
- Front-end compiler structure

---

## Program (token_counter.l)

```lex
%{
#include <stdio.h>

int keywordCount = 0;
int identifierCount = 0;
int numberCount = 0;
int stringCount = 0;
int logicalOpCount = 0;
int operatorCount = 0;
int delimiterCount = 0;
int commentCount = 0;
int unknownCount = 0;
%}

%%

\/\/[^\n]* { commentCount++; printf("COMMENT: %s\n", yytext); }

\/\*([^*]|\*+[^*/])*\*+\/ { commentCount++; printf("COMMENT: %s\n", yytext); }

int|float|char|double|void|if|else|while|for|return|do|break|continue|switch|case|default
{ keywordCount++; printf("KEYWORD: %s\n", yytext); }

[a-zA-Z_][a-zA-Z0-9_]* { identifierCount++; printf("IDENTIFIER: %s\n", yytext); }

[0-9]+(\.[0-9]+)? { numberCount++; printf("NUMBER: %s\n", yytext); }

\"([^\"\\]|\\.)*\" { stringCount++; printf("STRING: %s\n", yytext); }

&&|\|\| { logicalOpCount++; printf("LOGICAL_OP: %s\n", yytext); }

==|!=|<=|>=|<|>|[+\-*/%]=?|= { operatorCount++; printf("OPERATOR: %s\n", yytext); }

[{};,$begin:math:display$$end:math:display$()] { delimiterCount++; printf("DELIMITER: %s\n", yytext); }

[ \t\n]+ ;

. { unknownCount++; printf("UNKNOWN: %s\n", yytext); }

%%

int main() {
    printf("Enter code (Ctrl+D to end input on Mac/Linux):\n");

    yylex();

    printf("\n-- Token Counts --\n");
    printf("Keywords    : %d\n", keywordCount);
    printf("Identifiers : %d\n", identifierCount);
    printf("Numbers     : %d\n", numberCount);
    printf("Strings     : %d\n", stringCount);
    printf("Logical Ops : %d\n", logicalOpCount);
    printf("Operators   : %d\n", operatorCount);
    printf("Delimiters  : %d\n", delimiterCount);
    printf("Comments    : %d\n", commentCount);
    printf("Unknown     : %d\n", unknownCount);

    return 0;
}

int yywrap() {
    return 1;
}