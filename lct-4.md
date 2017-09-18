## Monday, 9/18 More on Variables + Arrays by Mansour Elsharawy

**Tech News!:** [ANDROID OREO FEATURES Y'ALL](http://www.androidauthority.com/android-8-0-review-758783/)

Aim: A vast array of possibilities

In the Do Now, we discussed with our partners any interesting, weird, or confusing things/issues we found while working on our Project Euler problems. Then we delved a more into variables in C!

### More on Variables!

First off, character literals can be denoted by single quotes instead of their numerical denomination.
Example: `char c = 'A';` and `char c = 65;` effectively do the same thing, but one is much more obvious as representing the character A.

String literals also exist, even though there is no String data type in C.
Example: `"Hello!"`

When declaring variables, the *order* in which you declare variables (and by extension, functions) matters.
Example...

```C

int i = 7;
int j = i + 1;
```
...is an entirely viable piece of code. *However...*

```C
int j = i + 1;
int i = 7;
```
...this will not work.

Variables also cannot be initialized in for loops in C, unlike Java, but can be initialized beforehand.

Example of proper for loopage:

```C

int i;
for(i = 0; i < 10; i++){
printf("i is %d\n",i);
}
```

Variables can also be declared as "unsigned," prohibiting the variable from taking on a negative variable.
This expands the range of values a variable can have, with 0 as the lower bound and a higher upper bound than an unsigned variable.
Example: `unsigned char x;` 0 <= x <= 255, where just `char x;` has -128 <= x <= 127

Booleans don't exist in C, but any variable with a value of 0 is regarded as false. *Any* other value evaluates to true.

Example of an infinite loop:
```C
while(1){
printf("To infinity and beyond!");
}

```

**IMPORTANT**
```C
int x=5;
if(x=6){
printf("foo");"
}
```
Even though the intended purpose of this code may be to skip the block containing the print statement, "foo" will be printed, as C will interpret the assignment of x to 6, which returns what x was assigned to (6), and that will evaluate as true.

Sometimes we may actually want this effect in the future!

### Memory Management

Memory allocation can happen at either compile or run time (as it is dynamic).
When the compiler sees you declaring a character variable for example, it will reserve 8 bits in memory for it, and is packaged with the binary of the program.

There is *no* default value for any variable. You get assigned a piece of memory which *might* be zero, but no guarantees!

We also briefly touched arrays, but the bell rang before we got anywhere meaningful besides the initialization:

```C
int l[5];
```
Cheers!



---
## Thursday, 9/14 Primitives by Jeremy Sharapov

**Interesting News:** [US bans Kaspersky software from government agencies](https://www.cnet.com/news/us-bans-kaspersky-software-from-government-agencies-trump-dhs-russia/)

**Bonus (I'm sick of Apple so here's some Google):** [Pixel 2 Launches on October 4th](https://arstechnica.com/gadgets/2017/09/google-teaser-site-promises-a-pixel-2-launch-on-october-4/)

Aim: Always read the fine print!

For our Do Now, we listed all of the primitives in Java, which are: 
* int
* char
* bool
* float
* double
* byte
* short
* long

In C we have all of them except bool and byte, and all of them are numeric, with the only differences between them being if they include floating points and the size of the variable in memory.
However, do note that the size can be platform dependent; use `sizeOf(<Type>)` to find the size in bytes.

|  Type  | Standard Size (in bytes) |                          Range                         |
|:------:|:------------------------:|:------------------------------------------------------:|
|  char  |             1            |                       -128 - 127                       |
|   int  |             4            |             -2,147,483,648 - 2,147,483,647             |
|  short |             2            |                    -32,768 - 32,767                    |
|  long  |             8            | -9,223,372,036,854,775,808 - 9,223,372,036,854,775,807 |
|  float |             4            |                    7 digit precision                   |
| double |             8            |                   14 digit presicion                   |

`printf()` - `stdio.h`
  * The most important C function
  * Prints formatted Strings
  * `printf(<String literal>, <var 1>, <var 2>, ...); `
  * Simple printf does not need the <var> arguments
  * printf does not add a newline at the end! Use `\n`
  * If you want to print variables, you must include formatting placeholders in the String argument
  * ex.
    ```C
    int i = 5;
    int main(){
      printf("i is %d", i);
      return 0;
    }
    ``` 
    print outs `"i is 5"`

|         Type        | Formatting Character |
|:-------------------:|:--------------------:|
|         int         |          %d          |
|         long        |          %ld         |
|        float        |          %f          |
|        double       |          %lf         |
|         char        |          %c          |
| char array (String) |          %s          |
|       Pointer       |          %p          |

---
## Wednesday, 9/13 Variables are the Spice of Life by Jennifer Zhang

**Interesting News:** [Apple Face ID](http://www.popsci.com/apple-face-ID)

* `man` is a command that will display a user manual
    * The manual is divided into sections (we talked about the first three):
        1. executable programs or shell commands
        2. system calls
        3. library routines
    * If you wanted to look up something from the manual, the command would be `man **keyword**`
        * For example:
            * `man ls`
            * `man man`
            * `man stdio`
    * Some functions may have the same name, and you might want to be able to specify which section the function you want is in.
        * For example, `man printf` will automatically give you the page for a printf in the 1st section. If you wanted to look up a printf from stdio, however, (stdio is in the 3rd section) you would instead type `man 3 printf`. (see below for more details)

If you recall from yesterday, when we ran our Hello World code, we were given a warning when using the function `printf()`:
* `printf()` is part of stdio, which is the standard input/output library.

When compiling your C code, `gcc` will go through two steps:
1. Checks if everything matches (syntax, function names, arguments and return type, etc.)
   * If it finds a function it does not see defined in the code, it assumes that you know what you're talking about, and will give you a warning.
2. Links the code for the external function
    * `gcc` can automatically link functions in standard libraries

Although warnings will still allow you to compile and run your code, it is ideal if your code has no warnings!

* `#include`
    * Include it in the header of your code
    * Put system libraries inside <>
    * Two major libraries we will be using:
        1. `#include <stdio.h>`
        2. `#include <stdlib.h>`

---
## Tuesday, 9/12 Hello, World! by Jake Goldman

**Interesting News:** [Can AI recreate a game engine?](https://www.digitaltrends.com/computing/ai-super-mario-bros-game-engine/)

**Bonus:** [Obligatory iPhone X hype](https://www.wired.com/story/apple-iphone-x-iphone-8/)

We began class by looking at a basic hello world program in C:

```C
int main(){
  printf("Hello Everybody!\n");
  return 0;
}
```
After running the code, we discussed several observations:
* The `main()` method in C doesn't have arguments
* `printf()` is used to print to the command line (it doesn't add a newline at the end)
* The `main()` method can have a return type (usually this will be an int and can indicate how a program terminated)

We then moved on to discuss why we use `./filename` to run C executables. In general, when one uses a command, the machine will search through certain directories stored in a variable known as PATH. As an example, when someone uses `ls`, the computer will go through each of the directories stored in PATH to find a file named `ls`, which will then be run. The computer only searches in these predetermined directories as a means of security, as certain programs could theoretically run themselves, leading to all kinds of potential issues. By specifying the directory of the executable we are trying to run, we are telling the machine that this is a safe file, and showing where to run it.

History of C:

The C language was developed by Denis Ritchie in the early 70s while working on UNIX at Bell Labs. The language ended up being the basis of the UNIX kernel, and in 1978, Ritchie along with Brian Kernighan published "The C Programming Language," which is considered to be one of the best books ever written about a programming language.

C Design Choices:
* C is designed to match very closely with machine level instructions (this creates leaner and faster programs)
* C is a procedural language (NOT object oriented)
* C syntax is very similar to Java syntax (Java syntax was based on C)

---
## Monday, 9/11 Basic C Code by Helen Ye

**Interesting News:** [Pluto's features are being named!](http://www.skyandtelescope.com/astronomy-news/first-pluto-features-officially-named/)

#### Aim: Let's C what you can do

Basic C code
* Source Code:
	* Put in .c files (convention)
	* Naming convention: snake_case
* Compiling (with command `gcc`)
	* Compiles to architecture specific (OS + Processor) executable files
	* Default name of compiled file is a.out
	* gcc option: -o \<file\> compiles to the given file name
	* Run file with ./\<file\>
		* C checks the $PATH for the file if you just type in the file name, unless you specify  it's directory

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
