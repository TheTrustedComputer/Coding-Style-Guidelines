# C/C++ Coding Style Guidelines #

I use a mixture of PascalCase, camelCase, and snake_case. It is important to know when to use them appropriately. If you do not follow my coding conventions, you may be asked to rewrite your code to conform to my coding style when I review pull requests. If you do not agree with the convention, you can suggest changes by creating a new issue. However, your changes may or may not be accepted if they deviate too much.

## Naming Conventions ##
* Structs, classes, unions, enums, and other similar constructs: PascalCase. Alias them with typedef when reusing them. They can be left without a name when they are nested. If that is the case, they are treated like variables.
```C
struct ThisStruct {
    struct {
        // ...
    } nestedStruct;
};
```

```C
typedef struct ThisStruct {
    struct {
        // ...
    } nestedStruct;
} ThisStruct;
```

```C
enum ThisEnum {
    // ...
};
```

```C
union {
    // ...
};
```

```C
// C only
typedef struct ThisStruct ThisStruct;
```

* Functions: camelCase. If it involves structures, insert an underscore between the struct name to be modified and the function name. Parameters are prefixed with an underscore. If the function has no parameters, explicitly use the "void" keyword, including main.
```C
int thisFunc(void) {
    return 1 + 2;
}
```

```C
// C
int ThisStruct_thisFunc(ThisStruct *_struct, int _param, const int _PARAM) {
    return _struct->a + _struct->b + (_param * _PARAM);
}
```

```C++
// C++
int ThisStruct::thisFunc(int _param, const int _PARAM) {
    return this->a + this->b + (_param * _PARAM);
}
```

```C
int main(void) {
    // ..
    return 0;
}

```
* Variables: camelCase. If it is a const, use SNAKE_CASE with all uppercase letters. For pointers, attach a space after the type name. If global variables are necessary, you may prefix it with a ``g_``. Although they are not mandatory, declare them as static whenever possible.

### Locals ###
```C
int thisVar;
```

```C
int *thisPtr;
```

```C
int thisVar, *thisPtr;
```

```C
const int THIS_VAR = 0;
```

### Globals ###
```C
static int g_thisVar;
```
```C
static int thisVar;
```
```C
static const int G_THIS_VAR = 0;
```
```C
static const int THIS_VAR = 0;
```


## Brackets ##
* Use K&R (Kernighan & Ritchie) style for bracket placement. The following points explain this placement.
* Opening brackets at the end of a function or expression must be on the same line, followed by a whitespace and this bracket.
```C
(expression) {

}
```

* Closing brackets needs to be on a new line by themselves.  When writing control flow statements, like "else" or "else if" in if statements, these brackets should be on a separate line.
```C
if (this) {
    // ...
}
else if (that) {
    // ...
}
else {
    // ...
}
```

```C
while (this) {
    // ...
}
```

```C
do {
    // ...
}
while (this);
```

```C
for (i = 0; i < 10; ++i) {
    // ...
}
```

## Indentation and Spacing ##
* As described above, prioritize K&R indentation over other styles.
* Four spaces. If there are tab characters, convert them to spaces first. Not all text editors format tabs equally.
* Case statements requires to be indented on the same line as switch statements.
```C
switch (this) {
case 0:
    // ...
    break;
case 1:
    // ...
    break;
}
```

* Always add a space between operators such as assignments, additions, and so on.
### Good ###
``z = x + y;``

### Bad ###
``z=x+y;`` ``z= x+y ;`` ``z = x+y;`` ``z= x + y;`` `z =  x + y;`

## Line Length ##
* There is no restriction on how long a single line of code can be. However, if it runs off to the right side of your IDE, consider wrapping it to the next line. I recommend 80 to 120 characters per line.

## Comments ##
* Provide detailed documentation at the top of the header file explaining what it does using multi-line comments.
```C
/*
    Document this header.
    
    Paragraph 1; Sentence 1.
    Paragraph 1; Sentence 2.
    
    Paragraph 2; Sentence 1.
    Paragraph 2; Sentence 2.
*/
```

* The function prototypes should have their own single-line comment, and the spacing of the prototypes and the comment should be consistent throughout the file. Adjust the spacing as you see fit.
```C
void f(void);       // Brief description of f()
void g(void);       // " " " g()
void h(void);       // " " " h()
```

* Write comments within functions for non-trivial things, but don't over-comment if it is fairly obvious to others.
* Use correct English spelling and grammar. There are online tools that can help you with this.
