# BNF Grammer

>here are BNF for our c_minus language

```
program : {glo_decl}+
glo_decl : enum_decl | var_decl | func_decl
enum_decl : 'enum' id '{' id '=''num' {',' id '=''num'} '}'
var_decl : type {'*'} id {'[' num ']'} {'=' num} { ',' id {'[' num ']'}{'=' num}} ';'
//Assign is allowed in var_decl
//ptr is default as NULL
//different from class-c every id's type is in the head

func_decl : type {'*'} id '(' func_para ')' '{' func_body '}'
func_para : type {'*'} id {',' type {'*'} id}
func_body : {var_decl} {stmt}

stmt : empty_stmt | no_empty_stmt
no_empty_stmt : if_stmt | while_stmt 
|'{' stmt '}' | 'return' exp ';'| exp ';' | decl_stmt
//declaration in stmt is allowed

if_stmt : 'if' '(' exp ')' stmt {else no_empty_stmt}
while_stmt : 'while' '(' exp ')' no_empty_stmt

reserve words:{"char", "int", "double", "else", "enum", "if", 
                "return", "sizeof", "while", "and", "or", "not"};
system function: {"open", "read", "close", "printf",
                "malloc", "memset", "memcmp", "exit"};

operator:   /, =, ==, +, ++, -, --, !, !=, 
            <, <=, <<, >, >=, >>, |, ||, 
            &, &&, ^, %, *, and, or, not
```

**notice:**  
- support multi-pointer(int***)
- support nest definition
- support assignment while definition
- support definition in statement
- identifier start with [_ | digit | alpha]
- funciton and its full definition must be put ahead of the caller
