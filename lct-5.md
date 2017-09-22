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
