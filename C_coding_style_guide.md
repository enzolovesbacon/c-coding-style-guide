# C coding style guide
===
    
This is my style guide for C programming.

I believe it makes my code well structured and clear enough for understanding.

<a name="Index"></a>
## INDEX

- [1. Font and Color](#FontAndColor)
- [2. Code Organization](#CodeOrganization)
- [3. Indentation, Tabs, Spaces and Newlines](#IndentTabsSpacesNewlines)
	- [3.1. Indentation and Tabs](#IndentTabs)
	- [3.2. Spaces](#Spaces)
	- [3.3. Newlines](#Newlines)
- [4. Comments](#Comments)
	- [4.1. When To Use Comments and Which One](#WhenUseComments)
- [5. Preprocessor Macros](#PreprocessorMacros)
- [6. Variables & Structs](#VariablesStructs)
- [7. typedef](#Typedef)
- [8. Functions](#Functions)
- [9. goto](#goto)
- [10. for, if, while](#If)
- [11. return](#Return)
- [12. Contact me](#Contact)
    
<a name="FontAndColor"></a>
### 1. Font and Color
[↑ top](#Index)

* Inconsolata, 12pt
* Color scheme [base16-default.dark.256](https://github.com/chriskempson/base16-iterm2/)

This is what I use for iTerm2 and I customized Xcode color scheme to look like the same.

<a name="CodeOrganization"></a>
### 2. Code Organization
[↑ top](#Index)

I separate my source code into several parts (I call them **sections**) so I easily know where to find something.

A file should be organized as follows:

1. License, credits and authors are described within a multi-line comment block
2. `#include`s
3. Preprocessor macros
4. External globals
5. Local globals (variables, `struct`s, etc)
6. Functions prototypes
7. Functions definitions

A `#pragma mark SOMETHING` might be used to separate sections.

<a name="IndentTabsSpacesNewlines"></a>
### 3. Indentation, Tabs, Spaces and Newlines
<a name="IndentTabs"></a>
##### 3.1 Indentation and Tabs
[↑ top](#Index)  

Tab width is 8. Source code gets a little wider, but it's much easier to read and navigate.

Tabs should only be used at "line start". Avoid using it elsewhere.

Also, I usually set a margin at 120 characters, but I don't always follow it.

Example:

    /* OK! */
    int function1(int a) {
    		if(a == 42)
	    			return 1;
	    	else
	    			return 0;
    }
    
    /* OK! */
    int a = 1;
    int foo = 3;
    int barbaz = 5
    
    /* NOT OK!!! */
    int var1		= 2;
    int variable2	= 4;
    int v3			= 8;


<a name="Spaces"></a>
##### 3.2. Spaces
[↑ top](#Index)

Spaces should be used very carefully to avoid misinterpretation:
    
    /* Example 1. OK! */
    void *function1(int *arg1, const char *arg2);
    
    /* Example 2. NOT OK!!! */
    void* function2(double* arg1, void* arg2);
    
    /* Example 3. NOT OK!!! */
    char * function3 (void* arg1 , int *arg2);

Allow me to explain "misinterpretation":
Example 1 is what I use and I think is the most correct because, although I avoid doing this, if you want to declare multiple pointers in a single line, you might miss something.

For example:  

    char *var1, var2;
    
I can clearly see that one char pointer and one char variable was declared. Now:  

    char* var1, var2;
    
I might misread it and think that two `char`s were declared.

That makes example 2 acceptable, but it's not what I follow neither recommend.

Example 3:
You're not even following a style. That makes code unreadable. I stop reading code right when I see something like that.

===

All functions, `if`s, `for`s, `while`s and etc, should all be followed by opening parentheses, with no spaces between them.

Actually, ALL parentheses and brackets should (almost) never contain any space before nor after it, unless it's a sub-expression.

    /* OK! */
    while(1);
    char str[100];
    while(function1(function2((&v)->var)))
    		
    /* NOT OK!!! */
    function (&var, 42)
    int array[ 2000 ];
    for ( i = 0; i < 100; i++ )
    function1( function2( 42 ) )
    
===

Most operators must be enclosed with spaces:

    /* OK! */
    a = 42;
    while((ptr != NULL) && i < 1000);
    a = b + c;
    if(x > y);
    x ^= (y & z) << d;
    
Operators that **should not** use spaces:

    /* OK! */
    ptr->var;
    i++;
    --x;
    function1(&v);
    function2(s.c);
    (float)var;
    if(!b);
    
Also, all casts should contain NO spaces:

    int a = (int)b;
    unsigned char *s = (unsigned char *)mem;
        
Explanation:
I ain't CodeGolfing or IOCCC'ing, so I find these the most appropriate form for my code.

<a name="Newlines"></a>
##### 3.3. Newlines
[↑ top](#Index)

Example:

    /* OK! */
    int function(int arg1, int arg2, char *arg3)
    {
    		int a = arg1 + 10;
    		int b = arg2 + 20;
    		
    		if(strncmp(arg3, "hell yeah!", strlen(arg3)) == 0) {
    				do {
    						printf("Woot!\n");
    						
    						if(a > 0)
    								a--;
    						else
    								a++;
    				} while(a != 0);
    				
    				return a + b;
    		} else if(strncmp(arg3, "oh no!", strlen(arg3)) == 0) {
    				if(a > 100)
    					return b;
    		} else {
    				switch(b) {
    						case 100:
    								return 0;
    						
    						case 40:
    								return -1;
    								
    						default:
    								b = b * 250;
    								
    								break;
    				}
    		}
    		
    		return a;
    }
    
* Function braces should be the only thing in their line;
* I put an empty line at each sub-section of a function (see [8. Functions](#Functions))
* Opening braces should be on the same line as their "owners" (`if`s, `for`s, `while`s, do-while blocks and switch-case statements, `struct`s declarations, etc)
* Closing braces should be the only thing in their lines, unless it's a do-while block, if-else or if-else-if statement

<a name="Comments"></a>
### 4. Comments
[↑ top](#Index)

Comments should be:  
  
    /* One line comment */  

Or:  

    // One line comment 2. I tend to avoid these for no particular reason.
  
Or:  
  
    /*
     * Multi-line comment block, 1 space before the text.
     *
     * Used for a longer text.
     * I use these to write things related to section 1 (see Organization), for example.
     */  

Or:  

     /*
      * 		Multi-line comment block, with 1 tab before the text.
      *
      *			I use these to describe a function's purpose.
      */

<a name="WhenUseComments"></a>
##### 4.1. When To Use Comments and Which One
[↑ top](#Index)

Comments might use a line for themselves **OR** be inlined, at the end of the line.

    void function(int arg1, /* Don't do this, this is bad */
    			  int *arg2, /* Don't do this, this is bad */
    			  char arg3)


- One line comment:
	
	Should be used to briefly explain what some specific line, or lines, of code is doing.
	
- One line comment 2:
	
	Personally I only use it to comment out code while debugging.
	
- Multi-line comment block:

    With 1 leading space before each sentence:
    - For file header comments - license, authors, credits, etc
    - For detailed explanation of a variable, code snippet, macro, etc
    - For when you think 1 line isn't enough
    
    With 1 tab before each sentence:
    - Section name ("External globals", "Local globals", "Prototypes", etc)
    - Summarized description of a function.
    
Any `#include` or macro that doesn't have an explicit reason of being there (name or known functionality), must be followed by a comment explaining its purpose.

<a name="PreprocessorMacros"></a>
### 5. Preprocessor Macros
[↑ top](#Index)

Macros identifiers must only contain A-Z uppercase and/or _ (underscore). It should be mostly self-explanatory and relatively not too long.

If you consider the token list to be long, it's ok to break the lines with '\'.

    /* OK! */
    #define DECLARE_VARIABLE(type, name, value) type name = value
    
    /* NOT OK!!! */
    #define F(a,b,c)((a)+(b)+(((b)>3)?(b):((a)>2)?(a):(c)))
    
<a name="VariablesStructs"></a>
### 6. Variables & Structs
[↑ top](#Index)

Any variable name must be a-z lowercase and might contain _ (underscores). Underscores are prefered instead of CamelCase.

Abbreviation is ok, as long as it makes sense, e.g.: `int retv` is prefered over `int returnValue`, or `int return_value`, or `int r`;

Global variables should be prefixed with "g_" for better understanding throughout the project.

Constant variables must only contain A-Z uppercase and/or _ (underscore). It should be mostly self-explanatory and relatively not too long.

Local variables that are going to be used for sure are prefered to be declared and initialized at start of scope.

Declaration doesn't necessarily implies initialization. For example, if you declare multiple variables of the same type, initializing one or more of them will make code less readable, being prefered to initialize one by one right after declaration.

    /* OK! */
    int a, *b, c, d;
    a = 4096;
    *b = malloc(4 * 1000);
    c = -5;
    d = 0;
    
    /* NOT OK!!! */
    int x, y = 10, z;
    
Structs should be declared at the "Global variables" section of the file.

<a name="Typedef"></a>
### 7. typedef
[↑ top](#Index)

**Never** typedef.

<a name="Functions"></a>
### 8. Functions
[↑ top](#Index)

Function names must be a-z lowercase and might contain _ (underscores). Underscores are prefered instead of CamelCase.

Abbreviation is ok, as long as it makes sense, e.g.: `proc(&val)` is prefered over `p(&val)`, or `process_and_update(&val)`;

I separate a function into "sections".

I call a section, each block of code that makes sense to be read together and these sections must be separated by empty lines. If this isn't clear enough, take a look at this example:

    int function(int arg1, char *arg2, double arg3)
    {
            /* This is what I would call the "variables section" */
            int x = -1;
            int y = -100;
            char *p1, *p2, *end;
            
            /* "functions section" */
            init(p1);
            init(p2);
            fetch_result(arg3, end);
            
            /* if, if-else, if-else-if, while, do-while section */
            if(p1 != NULL && p2 != NULL) {
                ((struct foo *)p1)->call(p2);
                
                /* "return section" */
                return x * arg3;
            }
            
            return y * arg3;
    }

<a name="goto"></a>
### 9. goto
[↑ top](#Index)

`goto`s might be used for function exit/cleanup. It's ok to be used for hacky stuff too, as long as you know what you're doing :)

    /* OK! */
    int function(char *string, int len, int flag) {
            char *s = malloc(len);
            int x = 0;
            
            if(FLAGS & flag) {
                    x = -1;
            
                    goto cleanup;
            }
            
            strncpy(s, string, len);
            x |= flag;
            
        cleanup:
            free(s);
            
            return x;
    }
    
<a name="If"></a>
### 10. for, if, while
[↑ top](#Index)

It is prefered to explicitly specify the condition. For example:

    /* PREFERED */
    if(ptr != NULL && len > 2048) {
            char *temp_ptr;
            
            for(temp_ptr = ptr; temp_ptr != NULL; temp_ptr++) {
                    [...]
            }
    }
    
    /* NOT PREFERED! */
    struct client *c = find_by_id(id);
    int count = 200;
    
    if(c) {
            while(count) {
                    process_client(c);
                    
                    count--;
            }
    }
    
The ternary operator `? :` should only be used by `return` statements. Otherwise, even for the shortest snippet of code, use an `if` block.

I prefer to arrange my code so I don't have to use `else`s.

    /* OK! */
    if(x > z)
            return x;
    
    return z;
    
    /* OK! */
    if(a < b)
            return b - a;
    else if(a == b)
            return a + b;
            
    return b;
    
    /* NOT OK!!! */
    if(x > z)
            return x;
    else
            return z;
            
        
<a name="Return"></a>
### 11. return
[↑ top](#Index)

Multiple `return`s are encouraged as most of times, you'll return some value if some condition is not met.

If the only purpose of a function is to check a condition, for example, then it's ok to use a ternary operator for that:

    int function(int *a, int *b)
    {
            return (*a > *b ? function2(a) : function2(b));
    }
    
Parentheses should be used if the return statement is an expression:

    /* OK! */
    [...]
    return (x + sin(y));
    
    /* NOT OK!!! */
    [...]
    return a > b;
    
<a name="Contact"></a>
### 12. Contact me
[↑ top](#Index)

Twitter or IRC: enzolovesbacon

===

<br><br>
(c) Enzo Matsumiya, 2014