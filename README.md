# Ex-4-LETTER-FOLLOWED-BY-ANY-NUMBER-OF-LETTERS-OR-DIGITS-USING-YACC
RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
# Date: 19-05-2026
# Aim:
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.
# PROGRAM:
### .l file:
```l
%{
#include "exp4_0007.tab.h"
#include <string.h>
%}

%%
[a-zA-Z][a-zA-Z0-9]*    { yylval.str = strdup(yytext); return IDENTIFIER; }
\n                      { return '\n'; }
.                       { return yytext[0]; }
%%

int yywrap() {
    return 1;
}
```

### .y file:
```y
%{
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

extern int yylex();
void yyerror(const char *msg);

%}

%union {
    char *str;
}

%token <str> IDENTIFIER

%%
start:
    IDENTIFIER '\n' {
        printf("Valid variable: %s\n", $1);
        free($1);  // clean up strdup memory
    }
    ;
%%

int main() {
    printf("Enter a variable name:\n");
    return yyparse();
}

void yyerror(const char *msg) {
    printf("Invalid variable name\n");
}
```

# Output:
### Commands:
<img width="886" height="130" alt="image" src="https://github.com/user-attachments/assets/7bfe81d0-1eb1-4ac7-8509-13a7fd0b7593" />

### Valid Case:
<img width="504" height="95" alt="image" src="https://github.com/user-attachments/assets/3b3e2635-a56a-4851-8446-b07c1baf24fa" />

### Invalid Case:
<img width="502" height="106" alt="image" src="https://github.com/user-attachments/assets/6064fe05-fa42-4443-b772-465fc000cae3" />


# Result
A YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.

### Name : ASWIN B
### Register Number : 212224110007
