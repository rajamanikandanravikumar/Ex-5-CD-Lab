# Ex-5-RECOGNITION-OF-THE-GRAMMAR-anb-where-n-10-USING-YACC
RECOGNITION OF THE GRAMMAR(anb where n>=10) USING YACC
# Date: 13-05-2025
# Aim:
To write a YACC program to recognize the grammar anb where n>=10.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the variables a and b.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a string as input and it is identified as valid or invalid.
# PROGRAM:
L file:
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
Y File:
```
%{
#include <stdio.h>
#include <stdlib.h>

int count = 0;
int yylex(void);
void yyerror(const char *s);
%}

%token A B INVALID

%%

input:
    valid_input '\n' {
        printf("Valid string\n");
        count = 0;
    }
  | INVALID '\n' {
        printf("Invalid string\n");
        count = 0;
    }
  | /* catch all other invalid formats */
    error '\n' {
        printf("Invalid string\n");
        yyclearin;  // clear current token
        yyerrok;    // reset error state
        count = 0;
    }
  ;

valid_input:
    A_seq B {
        if (count >= 10) {
            // valid
        } else {
            yyerror("Less than 10 a's before b");
        }
    }
  ;

A_seq:
    A           { count = 1; }
  | A_seq A     { count++; }
  ;

%%

int main() {
    printf("Enter strings:\n");
    while (yyparse() == 0);
    return 0;
}

void yyerror(const char *s) {
    printf("Invalid string\n");
}
```
# OUTPUT:
![image](https://github.com/user-attachments/assets/c00500cf-8d6b-48cc-bd81-46c644232851)

# RESULT
The YACC program to recognize the grammar anb where n>=10 is executed successfully and the output is verified.
