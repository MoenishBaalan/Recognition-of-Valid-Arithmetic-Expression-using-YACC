# Recognition-of-Valid-Arithmetic-Expression-using-YACC

## Register Number : 212223220057

## AIM   
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.

## PROGRAM
```Lex
%{
#include "ex03.tab.h"
#include <stdio.h>
%}

%%
[0-9]+        { yylval = atoi(yytext); return NUMBER; }
[a-zA-Z]      { return ID; }
[+\-*/=]      { return yytext[0]; }
[ \t\n]       ;
.             { return yytext[0]; }
%%

int yywrap() {
    return 1;
}

```

```y

%{
#include <stdio.h>
#include <stdlib.h>
%}

%token NUMBER ID

%%
stmt: expr { printf("Valid Expression\n"); }
    ;

expr: expr '+' expr
    | expr '-' expr
    | expr '*' expr
    | expr '/' expr
    | ID
    | NUMBER
    ;
%%

int main() {
    printf("Enter expression:\n");
    yyparse();
    return 0;
}

int yyerror() {
    printf("Invalid Expression\n");
    return 0;
}

```

## OUTPUT 
<img width="1031" height="473" alt="image" src="https://github.com/user-attachments/assets/ca6fd532-eba8-4ee3-be6b-23792c514bef" />

## RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
