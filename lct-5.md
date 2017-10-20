## Thursday, 10/19 : Get Dem Bugs by John Lin
**Interesting Tech News:** [Intel says Nervana computer chips will accelerate AI Revolution](https://www.cnet.com/news/intel-says-its-computer-chips-will-accelerate-ai-revolution/)

GDB
- Stands for GNU Debugger
- Tool for debugging a C program
- First compile the program, then call the gdb on the executable
```
gcc broken.c
gdb ./a.out
```
- In the GDB, you can start running the program by calling
```
run
```
- You can place a break point in the program by calling 
``` 
break line_number
```
- You can print the value of a variable by calling
```
print variable_name
```
- When a program stops at a break point, you can continue executing the program until the next break point by calling
```
continue
```

--------------------------------------------------------------------------------

## Wednesday, 10/18: back to the grind by Jasper Cheung
**Interesting Tech News:** [giant robot battle!!! WOW!](https://www.cnet.com/news/robots-megabots-twitch-suidobashi-battle-japan-usa/) [(vid)](https://www.youtube.com/watch?v=Z-ouLX8Q9UM) 

Valgrind
- tool for debugging memory issues in C
- (e.g. memory leaks, accessing freed memory, use of intialized memory) 
- You must complie with -g to use valgrind (and other similar tools)
``` 
gcc -g foo.c
```
- then you call valgrind when running the executable
```
valgrind --leak-check=yes ./a.out
```
- you may see different results when running valgrind on different OSs

---

## Friday, 10/13: Calloc and Realloc by Judy Liu

**Interesting Tech News:**[VR could trick stoke victims' brains toward recovery](https://www.cnet.com/news/vr-could-trick-stroke-victims-brains-toward-recovery/)

Calloc - clear allocation
```c
calloc (size_t n, size_t x);
``` 
- Allocates n*x bytes of memory
- Ensures that each bit is set to 0
- Works like malloc in all other ways

```c
int *p;
p = (int*) calloc (5, sizeof(int));
```

Realloc
```c
realloc(void *p, size_t x);
```

- Changes the amount of memory allocated in a given block
- Like free, p must point to the beginning of the block
- If x is smaller than the original size of the allocation, the extra bytes will be released
- If x is larger than the original size of size then:
 <p> 1. If there is enough space at the end of the original allocation, the original allocation will be updated </p>
OR
<p> 2. If there is not enough space, a new allocation will be created, containing the orginal values (copied over). The orginal allocation will be freed. </p>
  
```c
int *p;
p = (int *) malloc(10);
p = (int *) realloc(p,40);
```

--------------------------------------------------------------------------------


## Thursday, 10/12: "Malloc & Free: The dynamic duo" by Alexander Shevchenko

**Interesting Tech News:** [Facebook has launcehd a service through which its users can order food online](https://www.reuters.com/article/us-facebook-food/facebook-launches-u-s-food-order-and-delivery-service-idUSKBN1CI1UU)

Dynamic memory allocation:

```c
malloc(size_t x)
```
- Allocates x bytes of memory (from the heap)
- Returns the adress at the beginning of the allocation
- Returns a void * , always typecast to the correct pointer type


```c
int *p;
p = (int *)malloc(5 * sizeof(int));
```

```c
free(void *ptr)
```

- Releases dynamically allocated memory
- Takes one parameter, a pointer to the beginning of a dynamically allocated block of memory
- Every call to malloc/calloc should have a corresponding call to free

```c
int *p;
p = (int *)malloc(20);
free(p);
```

--------------------------------------------------------------------------------


## Wednesday, 10/11: "If you don't pay attention you'll get into a heap of trouble" by Jeffrey Lin

**Interesting Tech News:** [Google Will Hit 100% Renewable Energy this Year](https://web.archive.org/web/20171011014233/https://www.inverse.com/article/37308-google-renewable-energy-goal)

Recall the "stack trace diagrams" used for debugging to make sense of stack
memory.

We can attempt to make a linked list structure like so:

```c
#include <stddef.h> // declares NULL

struct node {
  int data;
  struct node *next;
};

struct node *insert_front(struct node *front, int d) {
  struct node new;
  new.data = d;
  new.next = front;
  return &new;
}

int main() {
  struct node *list = NULL;
  list = insert_front(list, 12);
  return 0;
}
```

Note that the compiler generates a warning:

```
tmp $ clang x.c                                                      
x.c:12:11: warning: address of stack memory associated with local variable 'new'
      returned [-Wreturn-stack-address]   
  return &new;       
          ^~~        
1 warning generated. 
```

The node is a piece of stack memory. When `insert_front` ends, *new* is popped off
the stack.
The value might still be there, but "might does not make right".

You need to use dynamically allocated memory to create a linked list.
Heap memory stores dynamically allocated memory.
Data will remain in the heap until it is released (or the program terminates).
Heap memory can be accessed through pointers, and can be accessed across many
functions.

--------------------------------------------------------------------------------

## Tuesday, 10/10: "If you don't pay attention you'll get into a heap of trouble" by Jeffrey Lin

**Interesting Tech News:** [Hacking is inevitable, so it's time to assume our data will be stolen](https://archive.is/EVOUi)

We use the `.` operator to access a value inside a struct.

```c
struct {int a; char x;} s;
s.a = 10;
s.x = '@';
```

You may not put a struct within itself, as that creates a compile-time error:

```c
int main() {
  struct foo {int a; char x; struct foo f;};
}
```

```
tmp $ clang x.c
x.c:2:39: error: field has incomplete type 'struct foo'
struct foo {int a; char x; struct foo f;};
                                      ^
x.c:2:8: note: definition of 'struct foo' is not complete until the closing '}'
struct foo {int a; char x; struct foo f;};
       ^
1 error generated.
1 tmp $
```

However, you may put a pointer to that struct within itself:

```c
int main() {
  struct foo {int a; char x; struct foo *f;};
}
```

This allows us to create a data structure similar to nodes and linked lists.

The `.` operation binds before the `*` operation.

```c
struct foo *p;
p = &s; // access the value of p.x using (*p).x
```

To access data from a struct pointer, you may also use `->`:

```c
p->x // same as (*p).x
```

You can typedef structs, but you must be careful as this will hide the fact that
you are working with a struct.

Moving on to stack memory versus heap memory:

Computer programs separate memory usage into two parts: the stack and the heap.
Every program can have its own stack and heap.

Stack memory stores all normally declared variables (including pointers and
structs), arrays, and function calls.
Functions are pushed onto the stack in the order they are called, and popped off
when completed.
When a function is popped off the stack, the stack memory associated with it is
released.

--------------------------------------------------------------------------------

## Friday, 10/3 | Finding your type | Arif Roktim

**Tech News:** [Google Fiber Scales Back TV Service To Focus Solely On High-Speed Internet](https://hothardware.com/news/google-fiber-scales-back-tv-service-to-focus-solely-on-gigabit-internet)

On Friday, we went over some commands involving types.

`typedef`: Provides a new name for an existing type  
Syntax: `typedef <real type> <new name>;`  
Reasons for using typedef include compatibility and readability.  
For example, strlen() returns type size\_t, which is typedef'd to `unsigned long`. It's clear that the function is returning a size.  
Usage:
```c
typedef long lolcat;
lolcat rainbow = 5;
```

We also went over `struct`. Structs are used to create a new type that is a collection of values.
Syntax:
```c
struct{ int a; char x; } var0;
struct{ int a; char x; } var1;
struct{ char *s1; char *s2; } var2;
printf("sizeof var0: %lu", sizeof(var0));
```
The type of variable `var0` is `struct{ int a; char x; }`.

It's annoying to have to type `struct{ int a; char x; }` over and over again so there is prototyping. Prototyping allows you to name a struct type.  
Syntax:
```c
struct foo {int a; char x;};
// struct foo is a prototype to be used later
struct foo s;
printf("sizeof s: %lu", sizeof(s))
```
Notice how the prototype has to be preceded by `struct`.

You can also make a prototype and instantiate a new variable at the same time:
```c	
struct bar {int a; char x;} t;
struct bar u;
```

We didn't go over how to access/modify the collection of values in a struct.

---

## Tuesday, 10/3 | Make it So | Asim Kapparova

**Tech News:** [drone deliveries using codes flashed from your phone’s LED](https://www.theverge.com/2017/10/4/16417986/delivair-drone-concept-led-flash-coded-cambridge-consultants)

Multiple File Compilation
- You can combine multiple C files into a C program by including them all in one gcc command.
-`gcc test.c string.c foo.c woohoo.c`
- You cannot have duplicate functions or global variable names across these files.
- Be careful: only one of these files should have a main 

Using `gcc -c`
- By using `gcc -c cfile.c` a file is created with the name cfile.o
- It is not a functional program, but it is compiled code.
- This is primarily used to compile c files without a main function.
- .o files can be linked with each other or with other c fiels by compiling them all at once.
- `gcc a.o b.c c.c`

Make
- Create compiling instructions and setup dependencies.
- Standard name used for make is makefile.

Syntax::
```make
<TARGET>: <DEPENDENCIES>
	<RULES>
```

For Example:
```make
all: dwstring.o main.o
	gcc -o strtest dwstring.o main.o

dwstring.o: dwstring.c dwstring.h
	gcc -c dwstring.c

main.o: main.c dwstring.h
	gcc -c main.c

clean:
	rm *.o
	rm *~

run: all
	./strtest
```

- Running a makefile: `make`
  - This will automatically make the first target. Which will recursively check if any dependencies need to be updated and then update them.
  - You can also include a target `make <TARGET>` and this will make the target specified recursively.
- The first target is typically a file that doesn't exist such that it is always updated.
- We also usually include a clean target to remove junk files and the like.
- Similarly we include a run target, that runs the final product.

Make is a good way to manage large processing of compiling/running code.

---
## Friday, 9/29 | Functions that Deal with Strings | Haoyu Chen

**Interesting Tech News:** [Belkin - Apple Dongle has lighthing port and headphone jack](https://www.theverge.com/circuitbreaker/2017/10/1/16393078/apple-belkin-rockstar-iphone-adapter-headphone-lightning)

**DO NOW**: Discuss the functions that you researched for homework with classmates
```C
#include <string.h>
char *strcpy(char *dest, char *src);
char *strncpy(char *dest, char *src, size_t n);
```
#### strcpy(), strncpy() : ####
These functions copy a string from one address to another, stopping at the NUL terminator on the srcstring.
strncpy() is just like strcpy(), except only the first n characters are actually copied. Beware that if you hit the limit, n before you get a NUL terminator on the src string, your dest string won't be NUL-terminated. 
Both functions return dest for your convenience, at no extra charge.
```C
#include <string.h>
int strcat(const char *dest, const char *src);
int strncat(const char *dest, const char *src, size_t n);
```
#### strcat(), strncat() ####
These functions take two strings, and stick them together, storing the result in the first string.
These functions don't take the size of the first string into account when it does the concatenation. 
Both functions return a pointer to the destination string, like most of the string-oriented functions.
```C
#include <string.h>
int strcmp(const char *s1, const char *s2);
int strncmp(const char *s1, const char *s2, size_t n);
```
#### strcmp(), strncmp() ####
strcmp() compares the entire string down to the end, while strncmp() only compares the first n characters of the strings.
Returns zero if the strings are the same, less-than zero if the first different character in s1 is less than that in s2, or greater-than zero if the first difference character in s1 is greater than than in s2.
```C
#include <string.h>
char *strchr(char *str, int c);
char *strstr(const char *str, const char *substr);
```
#### strchr(), strstr() ####
The functions strchr() finds the first occurance of a letter in a string
strchr() returns a pointer to the occurance of the letter in the string, or NULL if the letter is not found.
Let's say you have a big long string, and you want to find a word, or whatever substring strikes your fancy, inside the first string. Then strstr() is for you! It'll return a pointer to the substr within the str!
strstr() returns a pointer to the occurance of the substr inside the str, or NULL if the substring can't be found.

---

## Thursday, 9/28 | A string of functions | by Angelica Zverovich
**Interesting Tech News:** [Liquid Nitrogen Drives 18-Core Core i9-7980XE Above 6GHz](https://www.extremetech.com/computing/256623-liquid-nitrogen-drives-18-core-core-i9-7980xe-6ghz)

**DO NOW**: Write a function to find length of strings.

There are many possible ways to do this. 
Here is one example using bracket notation: 
```C
int length(char *s) {
  int i = 0; 
  while (s[i]) { //not necessary to write s[i] != 0 as the conditional because 0 is false in C
    i ++;
  }
  return i;
}
```
Here is another example using pointers:
```C
int length (char *s) {
    int i = 0; 
    while (*s++) { //you can imcrement the pointer in the while loop statement
        i ++;
    }
    return i;
  
}
```

Note that while it is possible to make the argument a char[] instead of a char * , any array is automatically passed as a pointer to the function, so there is no purpose in doing so. 

#### Declaring Strings ####
* `char *s2 = "Mankind"`  

   Creates immutable string "mankind" and returns a pointer to that string.You cannot modify strings created this way because the memory the pointer points to is immutable.

* You can only assign char arrays with = at declaration 

   `char s[] = "hello"; //ok!`             
   `s[] = "seven"; //NOT ok`

   Array are immutable pointers, you can't reassign an array pointer.

* Char pointers can assigned using = at any time 

    `char * s = "hello"; //ok!`                  
    `s = "seven"; //also ok!`            

---


## Wednesday, 9/27 cstrings by Eric Zhang

**Interesting Tech News:** [Some websites are using visitors' computers to mine cryptocurrency as an alternative to running ads](https://www.theguardian.com/technology/2017/sep/27/pirate-bay-showtime-ads-websites-electricity-pay-bills-cryptocurrency-bitcoin?CMP=twt_gu)

Today we used our knowledge of arrays and pointers to understand how strings work in c.

### Strings in c
Strings as character arrays
* Strings in c are simply character arrays.
* By convention, the last character in a string is a NULL character, denoted by `0`, or `'\0'`.
* This allows the end of a string to be found, as otherwise there is no way to find the length of an array.
* When printing a string, for example, everything from starting from the pointer location to the next null character is printed.

String literals
* When creating a string literal using `""`, an immutable string is created in memory, and is automatically null terminated.
* Consequently, all references to the same string literal reference the same immutable string in memory.

Declaring strings
* `char s[256];` is a normal array declaration, allocating 256 bytes to character array s.
* `char s[256] = "Imagine";` allocates the memory to s, then creates and copies the immutable string "Imagine", including the terminating null character.
* `char s[] = "Imagine";` creates the immutable string "Imagine", then allocates the appropriate amount of memory to s and copies it.

---

## Tuesday, 9/26 Let's Head to Function Town by Cesar Mu

**Interesting Tech News:** [Twitter just doubled the character limit for tweets to 280](https://www.theverge.com/2017/9/26/16363912/twitter-character-limit-increase-280-test)

Today we continued our discussion on passing by value and array variables, and learned of new ways to fix function declaration orders.

### Passing Arrays Into Functions
* Functions that take arrays as arguments can use pointer variables as their parameters.
```C
float arr[5];
foo(arr);

void foo(float *x){...} // *x will refer to the memory address of the array "arr"
```
* This works because array variables are inherently immutable pointers.

### Declaring Functions
* C is a procedural language, meaning that the order of the functions matters.
* Previously, we would just place any helper functions we needed at the top of the code and call it a day, but this will run into issues when we have cyclical functions that call on themselves.

* #### We have 2 better ways to fix this issue: 
    1. Declare the function header at the beginning of the code, then define later.
        * You don't need to provide names for the parameters, you just need the data types.
        ```C
        void print_array(int, int); // beginning of the code
        ...
        void print_array(int x, int y){...} // later on in the code
        ```
    2. Put the function headers in a separate file, then `#include` the header file.
        * When `#include`ing, the header file name must be in quotes.
        ```C
        // in "my_header.h"
        void print_array(int, int);
        
        // in "program.c"
        #include "my_header.h"
        ```

### Other Interesting Things
* An array variable points to a memory address, but that variable itself also has the same memory address.
* There is no way to determine what data type an array holds, because the collection of 0s and 1s in memory can be interpreted in any way, as int, float, double, etc.

---

## Monday, 9/25 How to Write Functioning Code, by Michael Lee

**Interesting Tech News:** [Poor coding limits IS hackers' cyber-capabilities, says researcher](http://www.bbc.com/news/technology-41385619)

We started class with Alex presenting his homework code. Many of us had code that looked something like this:
```C
int *p;
p = &array1[9-i];
array2[i] = *p;
```

While this code is correct, `&array1[9-i]` is redundant. If we do `array[index]`, that is shorthand for `*(array + index)`. A smarter way to do this would be `p = array + 9 - i`, which uses addition of pointers. 

Then we looked at an extreme case of C funkiness. Because array indexing is simply just pointer addition, the commutative property applies. Therefore:

```C
array[25]
```
and
```C
25[array]
```
yield the same result. However, good programmers would never do this because it is a headache to read.



#### Functions
C functions are structured similar to their java counterparts:
* returntype name(parameters){...}
Arguments are pass by values, meaning a copy of them is stored and used in the body of the function. This means if you have code like this:
```C
void foo(int a){
    a++;
}

int main(){
    int b = 3;
    foo(b);
    printf("%d\n", b);
    return 0;
}
```
the output value of b would still be `3`. 

---















## Wednesday, 09/20 Try Not to Hurt Yourself, the Point is Sharp by Jeffrey Luo

**Interesting Tech News**: [Researchers are using machine learning to predict earthquakes](https://phys.org/news/2017-08-machine-learning-earthquake-lab.html)

Today, we were introduced to pointers and how they work alongside memory addresses. Pointers are a relatively new concept as they aren't explicitly featured in Java. Below are the main points we covered in class.

### Pointers and their syntax
* Pointers simply are variables that store a memory address.
* Because they're used to store addresses, all pointers are the same size, regardless of type. Typically, they are either 4 or 8 bytes large depending on architecture (32 vs 64 bit).
* Pointers are denoted by using the asterisk (`*`).
* Memory addresses can be obtained by using the ampersand (`&`) before the variable. Ex: `&a` returns the address of variable `a`.
* Addresses stored in pointers can be printed using the `%p` format modifier. Ex: `printf("%p\n", p)` prints the memory address of pointer `p`.

Example:
```C
int x = 4;
int *ip; // creates an integer pointer
printf("Address of x: %d\n", &x); // prints "Address of x: 15288" (for the sake of this example)
ip = &x; // initializes pointer 'ip' by assigning it the address of variable 'x'
```
We can the visualize the above as:

|         |    x    |       ip     |
|--------:|:-------:|:------------:|
|  Value  |      4  |     15288    |
| Address |  15288  | (not needed) |

* Pointers can be dereferenced  also by using the asterisk (`*`). This returns the value of the data which the pointer points to. Continuing from above:
```C
printf("Value of x: %d\n", *ip); // prints "Value of x: 4"
```
* Finally, remember that pointers themselves have memory addresses! After all, they are variables themselves.

### Pointer Arithmetic

* As pointers store memory addresses, they can be incremented at a size corresponding to the data type. Because of this, we can access different memory addresses relative to the initial memory address.
Example: 
```C
int a = 10; 
int *ip = &a;
char b = 'a'; 
char *cp = &b;
ip++; // increments ip by 4 bytes (size of int)
cp++; // increments cp by 1 byte (size of char)
```


---

## Monday 09/18 Data Types and Variables By Daniel Regassa

**Interesting Tech News**: [Intel is working with Waymo to build fully self-driving cars](https://www.theverge.com/2017/9/18/16328284/intel-waymo-partnership-self-driving-car-chrysler)

### Character and String Literals
* Just to refresh our memories, in programming languages a literal is a value that can never be changed after
    it is declared, while on the contrary, a variable represents a value that can be redeclared indefinitely.
* In C, there exist both character and string literals (even though there is no "string" data type)
* Character Literals are delimited by single quotes like so: `'a'`
* String Literals are delimited by double quotes like so: `"hello, world!"`

### Unsigned Integers
* All variables of the primitive data types can be initialized with the `unsigned` keyword at the front
* Ex: `unsigned int foo = 42;` 
* Unsigned variables can only take up non-nengative values
* They can hold up to twice as many positive numbers as their "signed" counterparts
* For example, a char can hold the values from -128 to 127, while an unsigned char can hold the values 0 to 255

### Booleans
* Unlike other programming languages like Java or Python, there is no boolean data type.
* Instead, in C we use integer values for booleans
* `0` corresponds to false, and any other integer corresponds to true

**WARNING**: Don't do this unintentionally: 

 `if(x = 6){...}` 

When you mean to do this: 

 `if (x == 6){...}`

As in the former the assignment operator will return the value of the integer literal, in this case 6, which will always
be interpreted as true.

### Memory Management (to be continued in the next lesson)
* Memory in C is allocated either at compile time (static memory) or run time (dynamic memory)

#### Compiler Allocated Memory
* Packaged with the compiled binary file
* The variables and arrays we have been using so far use this type of mamory
* Variables not have a standard default value, like they would in other languages like Java (the default being `0` for many 
data types)
- Instead a variable that has not been declared yet will use whatever value already resides in that spot in memory
- This is because C's philosophy is to do only exactly what we tell it to, and auto-declaring every variable to a default
value would be a wasteful operation. C assumes that if we wanted to set something, we would on our own

---

## Thursday 09/14 Always Read the Fine Print By Ricky Chen

**Interesting Tech News:** [OpenAI bot beats professional DoTA2 players.](https://blog.openai.com/dota-2/) [(Further reading)](https://blog.openai.com/more-on-dota-2/)

Do Now: List the Java primitives.
* int
* double
* float
* char
* long
* short
* byte
* boolean

### All About C Primitives
In C, there are no byte or boolean primitives. All C primitives are numerical, which means that char is expressed using ASCII.

These primitives differ in both their sizes and the content which they can store. int, short, and long are used for integers while double and float are for floating point numbers. The following table should give insight into the the size of each primitive:

| Primitive | Size (Bytes)| Range |
| ------------- |:-------------:| -----:|
| int | 4 | ~ -2 billion to 2 billion |
| char | 1 |    |
| double | 8 | |
| float | 4 |  |
| long | 8 | 14 digits of percision |
| short | 2 | 7 digits of percision |

### All About Printf
The function `printf(<string literal>, var1, var2...)` is essential to the C library. It is found in the stdio.h library and can be used by adding `#include <stdio.h>` to your code.
The function itself can take one argument that must be a string, **not a variable.** If you wish to append a variable to an existing string, you may do something like the following:
```C
int i = 29;
printf("The number is: %d\n", i);
```
Notice the use of `%d`. This marks the spot for which the variable will be placed into the string. `%d` is not universal formatting for all data types; thus that the following table should be of use:

| Type | Formatting|
| ------------- |-------------:|
| int | %d |
| char | %c |
| double | %lf |
| float | %f |
| long | %ld |
| pointer | %p |

As a side note, int is paired with `%d` due to it being a *d*ecimal number.

Following this, we were asked to create a C program that would first print a variable correctly and then incorrectly. This was my code for correctly:
```C
#include <stdio.h>

int x = 42;
double y = 28.6668;
char z = 's';

int main(){
    printf("Int is: %d\n", x);
    printf("Double is: %lf\n", y);
    printf("Char is: %c\n", z);
    return 0;
}
```
This was what was shown in the terminal:
>Int is: 42

>Double is: 28.666800

>Char is: s

Now, for doing it incorrectly, I modified my main class to be:
```C
int main(){
    printf("Int is: %lf\n", x);
    printf("Double is: %c\n", y);
    printf("Char is: %d\n", z);
    return 0;
}
```
Which resulted in:
>Int is: -0.026042

>Double is:

>Char is: 115

Interesting to note is that I did not get a warning for the third printf call.

---

## Wednesday, 9/13 If Variables are the Spice of Life, Then are They SpiceC? By Queenie Xiang

**Interesting Tech News:** [Facebook's Artificial Intelligence Robots Get "Shut Down"](http://www.independent.co.uk/life-style/gadgets-and-tech/news/facebook-artificial-intelligence-ai-chatbot-new-language-research-openai-google-a7869706.html) 

The aim for today's class was "Variables are the spice of life." Our do now was to run <pre><code>$man stdio</code></pre> and share what we learned. 

We found out that this displayed the manual and documentation for stdio. It shows the name, library, synopsis, description, standards, list of functions, and bugs.

Generally, <code>man</code> represents the manual where you can look up the details of a command or program you're not familiar with. So for example, if you wanted to look up the documentation on <code>ls</code>, you would type in <pre><code>$man ls </code></pre> Each command/program has a section of the manual it belongs to. The number of the section appears in the top right corner. 

To look up something in a particular section: 
<pre><code> man section# command/program_name </code></pre> 
For example, <code>printf</code> exists in many sections. If you wanted to look at the <code>printf</code> in section 3 instead of section 1, you would type:
<pre><code>$man 3 printf</code></pre>

In the manual, if <code>...</code> is in a function headline, it means the function can take an arbitrary number of arguments. 

To include librarys and use functions defined in other files:
* (1) Check that you're using the function correctly: the arguments and return type must match what the function defined.
* (2) Link the code for the external function to your executeable code: GCC can automatically link functions in standard libraries and it grabs ONLY what is needed. 

Use: <pre><code> #include </code></pre> (used during step 1 above) 
* Used to include function headers with your code: this tells the compiler to look and check for these functions. 
* It is necessary to match arguments and return type.
* It's not necessary for linking(step 2 above).
* If it's a standard C library, use angle brackets: <pre><code> <standard_c_library_name> </code></pre> (otherwise, don't). 

An example of this would be:
```C 
#include <stdio.h>
``` 

By the way, the # in <code> #include </code> allows the include to be interpreted before all other code. 

---  

## Tuesday, 9/12 The ABCs of C by Michael Cheng

**Interesting Tech News:** [Meet the iPhone X, Apple's New High-End Handset](https://www.wired.com/story/apple-iphone-x-iphone-8/)

We started class by creating the classic "Hello, World!" program in C:
<pre><code>int main(){
   printf("Hello, World!\n");
   return 0;
}</pre></code>

After compiling with <code>$ gcc hello.c</code> and executing with <code>$ ./a.out</code>, the resulting output was <code>Hello, World!</code> with a newline at the end. There is no <code>println()</code> in C, so a newline must be added manually, if desired.

We noticed that there are striking similarities to Java, such as in syntax, with the are curly brackets and semi-colons. C also requires a main function, similar to Java, but note that it is not a facsimile of Java's, as shown above. The main function must return a value. Furthermore, C is a procedural language, not an object-oriented language.

We then went over the reasons why <code>./</code> is used when executing C programs. For one, it is used for security, and because it is shorthand for the current directory. An error will occur if <code>./</code> is not used, as bash will look for the command in locations described in the <code>$PATH</code> environmental variable only.

Then we had went over briefly on the history of C:
* C was developed at Bell Labs by Dennis Ritchie in the early 70s while he was working on UNIX. C was then used to rewrite UNIX.
* Dennis Ritchie and Brian Kernighan published *The C Programming Language* in 1978, a reference book for the C programming language.

---  

## Monday, 9/11 Jumping into the C by Daria "Dasha" Shifrina

**Interesting Tech News:** [Robot Learns to Follow Orders like Alexa](http://news.mit.edu/2017/robot-learns-to-follow-orders-like-alexa-0830)

Today, we were introduced to C for the first time. We started off by contrasting Java and C. Unlike C, Java provides a JVM(java virtual machine) that compiles your code to run in different computing environments. In C, you do not have a virtual machine so you must manually recompile when switching between operating systems.

Then, we learned that there are several conventions when it comes to C:
* Put in .c files
* snake_case 
Ex: black_mamba.c

We also learned how to compile a C file. To compile, you must use the gcc(gnu c compiler). One "inconvenience" of C is that it doesn't recognize your file name when you compile the code, instead creating an output file called "a.out", which stands for "assembler output." There are ways to change that output file name. Here's an example of what you'd write in your terminal if you were trying to compile black_mamba.c:
<blockquote>
   
    $ gcc black_mamba.c #Creates a.out files  
    
    $ ./a.out #output of black_mamba.c  
   
    $ gcc -o snake black_mamba.c #rename a.out to snake  
   
    $ ./snake #output of black_mamba.c
</blockquote>

---

## Wednesday, 9/6 Blissfull respite, I hardly knew ye by Clyde "Thluffy" Sinclair

**Interesting Tech News:** [Do You Even Olin?](https://blog.ledwards.com/the-college-that-produces-founders-at-3-times-the-rate-of-stanford-2c53ea44f91e)

Don't forget, each new post should go above the one before. If you are late in posting, please put yours in the correct position.

#### Look, it's a list! ####
* Blah
* Blah
* Blah

Below you'll find a horizonal bar, please put one at the end of your post.

---
