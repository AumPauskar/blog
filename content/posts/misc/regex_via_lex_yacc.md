+++
title = 'Regex via lex and yacc'
date = 2024-06-06T08:55:38+05:30
tags = ["regex", "lex", "yacc", "compiler", "parser"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Desc Text."
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# Regex via lex and yacc

## What is a regex?
Regular expressions (regex) are patterns used to match character combinations in strings. In JavaScript, regular expressions are also objects. These patterns are used with the exec() and test() methods of RegExp, and with the match(), matchAll(), replace(), search(), and split() methods of String.

## Why use lex and yacc?
Lex and yacc are tools used to generate lexical analyzers and parsers. Lex reads an input stream specifying the lexical analyzer and outputs source code implementing the lexer in C. Yacc reads an input stream specifying the parser and outputs source code implementing the parser in C. Lex and yacc are tools used to generate lexical analyzers and parsers. Lex reads an input stream specifying the lexical analyzer and outputs source code implementing the lexer in C. Yacc reads an input stream specifying the parser and outputs source code implementing the parser in C.

## Example programs

### Example set 1
- **Title:** Lexical program to count lines and add the line numbers
- **Algoritm:**
    1. Start the program. If a command-line argument is provided, it is assumed to be the name of the input file. If no argument is provided, the program reads from standard input.
    2. Initialize a variable `line_num` to 1. This variable keeps track of the current line number.
    3. Start the lexical analysis with the `yylex()` function. This function reads the input and applies the first rule whose pattern matches the current input.
    4. Check the current input against the following rule:
    - If the input matches the pattern `^.*\n` (an entire line), print the line prefixed with its line number and increment `line_num`.
    5. Repeat step 4 until the end of the input is reached.
    6. When the end of the input is reached, call the `yywrap()` function. This function returns 1, indicating that the lexer should stop.
    7. End the program.
- Code
```c
%{
#include <stdio.h>
int line_num = 1;
%}

%%
^.*\n  { printf("%d %s", line_num++, yytext); }
.   { ECHO; }
%%

int main(int argc, char **argv) {
    if (argc > 1) {
        FILE *file = fopen(argv[1], "r");
        if (!file) {
            perror(argv[1]);
            return 1;
        }
        yyin = file;
    }
    yylex();
    return 0;
}

int yywrap() {
    return 1;
}
```
- How to run
```bash
lex program.l
gcc lex.yy.c -o program -ll
./program < input.txt
```
In order to get the output in a file the following command may be run
```bash
(./program < input.txt) > output.txt
```

- **Title:** Yacc program to parse arithmetic expressions and find out validity
- Yacc code
```c
%{
#include <stdio.h>
#include <stdlib.h>
void yyerror(const char *s);
int yylex();
%}

%token NUMBER PLUS MINUS MULTIPLY DIVIDE LPAREN RPAREN

%left PLUS MINUS
%left MULTIPLY DIVIDE

%%

expr:
      expr PLUS expr       { printf("PLUS\n"); }
    | expr MINUS expr      { printf("MINUS\n"); }
    | expr MULTIPLY expr   { printf("MULTIPLY\n"); }
    | expr DIVIDE expr     { printf("DIVIDE\n"); }
    | LPAREN expr RPAREN   { printf("PARENTHESIS\n"); }
    | NUMBER               { printf("NUMBER\n"); }
    ;
%%

void yyerror(const char *s) {
    fprintf(stderr, "Error: %s\n", s);
}

int main() {
    printf("Enter an arithmetic expression:\n");
    yyparse();
    return 0;
}
```

- Lex code
```c
%{
#include "y.tab.h"
%}

%%
[0-9]+        { yylval = atoi(yytext); return NUMBER; }
[ \t\n]+      ; // Ignore whitespace
"+"           { return PLUS; }
"-"           { return MINUS; }
"*"           { return MULTIPLY; }
"/"           { return DIVIDE; }
"("           { return LPAREN; }
")"           { return RPAREN; }
.             { return yytext[0]; }
%%

int yywrap() {
    return 1;
}
```
- Algorithm
    1. Start the Yacc program with a `%{...%}` block. This block is for C code that gets copied verbatim to the generated C source file. Include the necessary header files (`stdio.h` and `stdlib.h`) and declare the functions `yyerror` and `yylex`.
    2. Define the tokens that will be used in the grammar rules. These might include `NUMBER` for numeric literals and `PLUS`, `MINUS`, `MULT`, `DIV` for the arithmetic operators.
    3. Define the grammar rules for valid arithmetic expressions. Here's a simple example:
    - An expression can be a `NUMBER`.
    - An expression can be another expression followed by a `PLUS` token and then another expression.
    - An expression can be another expression followed by a `MINUS` token and then another expression.
    - An expression can be another expression followed by a `MULT` token and then another expression.
    - An expression can be another expression followed by a `DIV` token and then another expression.
    - An expression can be enclosed in parentheses.
    4. For each grammar rule, define an action that gets executed when the rule is applied. If you're only checking the validity of the expression and not evaluating it, these actions can be empty.
    5. Define the `yyerror` function. This function is called when a syntax error is encountered. It should print an error message and possibly terminate the program.
    6. End the Yacc program with a `main` function that calls `yyparse()`. This function starts the parsing process.
    7. Compile the Yacc program with `yacc -d`, compile the Lex program with `lex`, and then compile the generated C code with `gcc`. Run the resulting program with an input file to check the validity of the arithmetic expressions in the file.
- How to run
```bash
yacc -d program.y
lex program.l
gcc y.tab.c lex.yy.c -o program -ll
./program
```