## Tuesday, 9/19 | What's the point of it all? | Grace Cuenca

**Interesting Tech News:**  [Twitter Cracking Down on Accounts Promoting Terrorism](http://money.cnn.com/2017/09/19/technology/business/twitter-transparency-report/index.html)

## Memory Management 
* Memory allocation either happens at compiler time or at run time (dynamic)
* Compiler allocated memory:
  * Packaged with the binary of the program
  * There is no standard default value (unlike Java). This is because C doesn't "zero out" anything. This saves processing time.
  * Variables and arrays are allocated here

Example:
```C
float a
int b[5] //when you do this, you ask the operating system to give you an array of 5 integers. 
//The memory is allocated when it's compiled, not when it's run
```
## Arrays
* Must have a fixed size set at declaration
 * However, there is memory before and after the allocation
 * There is no error that appears if you go beyond the array size (either before or after)
 ```C
 b[6]
 b[-2]
 //both will not cause errors
```
 * **NOTE:** In accessing memory beyond the array, you may run into this error:
 ```C
segmentation fault (core dump) //the function is trying to access memory that it's not allowed to
```
* When you ask for an array in C, you're asking the operating system for a contiguous block of memory of a certain size
* There is no length function
* There is no boundary checking

---

## Monday, 9/18 | Data Types and Variables | Sabrina Wen

**Interesting Tech News:**  [Computers and Human Brains!](https://nyti.ms/2y5xcLS)

We spent the first half of class talking about how to submit homework assignments by using submodules (basically links to separate repositorys), and the second half going over data types and variables in C.

### How to use submodules to submit homework assignments:

1. First, make a *separate repository* for every homework assignment. 
2. When you commit your repository (or any other repository for that manner), it's recommended that you use the flags `-a -m`. For example: 
```
git commit -a -m "This is a commit msg!"
```
3. Clone the master repository (aka the class assignment respository) and make sure to use the HTTPS link.
4. Use the following to add your submodule to the master repository:
```
git submodule add *insert HTTPS link wow!*
```
5. Commit and push your file as your normally would. You can also remove the master repo from your computer if you want to.

### Data Types and Variables 
* Character literals are single characters inside `''`. Ex: `'a'`, `'b'`
* String literals exist, even though there is no string data type. Ex: `"hello"`, `"hi there"`
* Note that `%s` is the placeholder for a string literal.

* The order that identifiers are declared is important. This includes functions, which must also be declared before they are used.
* Variables can't be declared inside for loop statements, but they can be initializeD. Ex:
```C
int a;
for (a = 0; a < 10; a++) { 
    printf("hi\n");
}
```
* Any variable type can be declared as an "unsigned" variable. This means the variable will never be negative.
	1. The lower bound of any unsigned variable is equal to 0.
	2. The upper bound of any unsigned variable is greater than the unsigned version.
Ex: `unsigned char x;` where 0 <= x <= 255
* All boolean values are numbers. 
	1. 0 --> false
	2. anything else --> true

**NOTE:** Since boolean values are represented by numbers, it's easy to trigger an infinite loop. For example:
```C
if (x = 6) {
    do stuff
}
```
Because x is assigned to the variable 6, the boolean value in the if statement will always be true.


---

## Thursday, 9/14 | Always read the fine print | Ahbab Ashraf

**Interesting Tech News:** [Iphone X? Never heard of it](https://www.theverge.com/2017/9/14/16306472/google-pixel-2-launch-date-october)

We spent most of the class discussing primitives in C, which largely are the same as in Java. However, both booleans and bytes are excluded in C. Below is a table of the 6 types of primitives, with other important info:

| Primitive | Size(bytes) | Range |
|:---:|:---:|:---:|
| char | 1 | -128 to 127 | 
| int | 4 | ~-2 billion to ~2 billion |
| short | 2 |  |
| long | 8 |  |
| float | 4 | 7 digit precision |
| double | 8 | 14 digit precision |

#### More about primitives
* All primitives are numeric
* They differ in both their sizes and their type of numerical information (floating point vs integer)
* If you want to find a primitive's size on the fly, you can use ``sizeof(TYPE)`` (from stdlib.in)

We also talked about `printf` and formatting placeholders. This is a way of printing variables more easily than in Java. Here's an example:

```C
int i = 5;
printf("i is %d", i);
```

In this case, `%d` is the placeholder variable for the integer `i`. For every placeholder, there must be a corresponding value in the function call. Below are a number of placeholders and their corresponding data types:

| Type | Placeholder |
|:---:|:---:|
| int | %d |
| long | %ld |
| float | %f |
| double | %lf |
| char | %c |
| char array | %s |
| pointer | %p |

**NOTE:** For doubles, `%0.<x>` can be used as a placeholder as well, printing with x digits after the floating point.

---

## Wednesday 09/13 Variables are the spice of life by Jake Zaia

**Interesting Tech News:**  [Solar panels are getting cheaper faster than expected!](https://arstechnica.com/science/2017/09/solar-now-costs-6-per-kilowatt-hour-beating-government-goal-by-3-years/)

We spent the day discussing libraries in C, and how to include them in our programs, as well as how to utilize the `man` command to its full potential.

### Things to know about `man`
* `man` is short for "manual", the whole manual of how to use Linux (Or OS X) comes with the computer and is *in* the computer
* `man` also has pages for C, detailing libraries and commands
* The manual is split into 9 sections, and to locate each one, you can read the man page for man (`$ man man`)
* To view a specific section of the man pages, you can pass it the section as a parameter. ex. `$ man 3 printf` will check the 3rd section of the man pages for the page about "printf"

### Things to know about including libraries in C
* Upon compiling C does 2 things to use library functions
	1. Checks the function for syntactic use to make sure it is legal
	2. Links the code for the external function (and ONLY that function) to your executable
* To include a library in C, you write `#include <libraryname>` including the angle brackets/gang signs 

---

## Tuesday, 09/12 Hello, world by Jeffrey Weng

**Interesting Tech News:** [Iphone X hype?](https://www.theverge.com/2017/9/12/16291244/new-iphone-x-photos-video-hands-on)

We were told to copy a simple Hello World program in C and compile it:

```C
int main(){
  printf("Hello Everybody!\n");
  return 0;
}
```

We also made some distinctions between C and Java:
* No public/private access modifiers
* No classes
* Not `System.out.println()` but `printf()` *(Note: `printf()` doesn't include a new line)*
* `main()` instead of `public static void main(String[] args)` 
* We also touched on the idea of returning 0 instead of using a void function because it shows that the function has ran correctly


**IMPORTANT**: C is a imperative/procedural programming language while Java is a OOP language


*Calling our compiled file requires us to use `./<filename>` when we're in the same directory as the file instead of calling just the `<filename>`*
#### Why?

For example if we were to change our filename to a common command such as `ls`, which displays the files in your current directory, how do we determine the difference?

While calling `ls` we access an environmental variable called **PATH**, which tells the shell which directory to look for the ls program. Note this doesn't call our *ls program* but the
compiled C program in the system.

To call our *ls program* we would specify which directory it is in, to override our **PATH** environmental variable. 

Doing this provides us extra security as it stops regular users from manipulating common commands such as `ls` and helps us differentiate similarly named programs.

#### Useful Commands

`which [-option]` - Searches the path of executable in system paths set in $PATH <br />
`echo` - you can use this to either *echo* a string you input or if you provide an environmental variable, show the values of the environmental variable

Examples of `echo`
1. `echo Hi`
Terminal spits out: Hi
2. `echo echo`
Terminal spits out: echo
3. `echo $PATH`
Terminal spits out: a series of colon-separated paths

OPTIONAL TEXTBOOK: The C Programming Language by Brian Kernighan and Dennis Ritchie


---

## Monday, 09/11 Venture into the C by Jen Yu

**Interesting Tech News:** ['The New Yorker' on Hyperloops](https://www.newyorker.com/tech/elements/hypnotized-by-elon-musks-hyperloop)

We learned the basics of C programming by creating a file and compiling it. Here are the steps to creating your very own executable C file: 
1. Write source code in a text editor and save with the `.c` extension. <br>
	* **Note**: The naming convention for C is **snake_case**, _where all words are lowercase and distinct words are separated by underscores._ 
  
2. Open the command line and type in `gcc <filename>`. <br>
	* **gcc** stands for "GNU C Compiler", and compiles the file to the architecture specific (OS + Processor) executable file. 
  
3. ``ls`` to list the files in your current directory. 
   * You will see an ``a.out`` file, which is the default name of a compiled file in the C programming language. 
4. Run the executable file: `./a.out`

OPTIONAL BUT **HIGHLY** RECOMMENDED <br>
Rename your `a.out` file! Despite it being the default name, it's by no means descriptive and will be overwritten if another C file is compiled within the same directory. <br><br>
To do so: <br>
``gcc -o <new_filename> <filename>``<br> 
\* `new_filename` does not include an extension. 
<br><br>
Example: <br>
If I did: `gcc -o hi hello.c`<br>
I rename the compiled hello.c to `hi`.

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
