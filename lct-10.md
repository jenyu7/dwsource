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
