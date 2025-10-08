# Ex.No:5
# RECOGNITION OF THE GRAMMAR(a^nb where n>=10) USING YACC
## Register Number:212224040362
## Date:06/10/2025
## AIM:
To write a YACC program to recognize the grammar a^nb where n>=10.
## ALGORITHM:
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the variables a and b.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a string as input and it is identified as valid or invalid.
## PROGRAM:
expr5.l
```
%{
#include "expr5.tab.h"
%}

%%

a       { return A; }
b       { return B; }
\n      { return '\n'; }
.       { return INVALID; }

%%
int yywrap() {
    return 1;
}
```
expr5.y
```
%{
#include <stdio.h>
#include <stdlib.h>

int count = 0;  // count of 'a's
int yylex(void);
void yyerror(const char *s);
%}

%token A B INVALID

%%

input:
    A_seq B '\n' {
        if (count >= 10) {
            printf("Valid string: a^n b where n >= 10\n");
        } else {
            printf("Invalid: less than 10 'a's before 'b'\n");
        }
        count = 0; // reset for next input
    }
  | INVALID '\n' {
        printf("Invalid character in input.\n");
        count = 0;
    }
  ;

A_seq:
    A           { count = 1; }
  | A_seq A     { count++; }
  ;

%%

int main() {
    printf("Enter strings (e.g., aaa...ab), one per line (Ctrl+D to quit):\n");
    while (yyparse() == 0);
    return 0;
}

void yyerror(const char *s) {
    // Errors handled in grammar
}
```
## OUTPUT:
<img width="931" height="769" alt="image" src="https://github.com/user-attachments/assets/af92a97c-f35e-4cb8-b0e6-03ff0dcf9450" />




## RESULT:
The YACC program to recognize the grammar anb where n>=10 is executed successfully and the output is verified.
