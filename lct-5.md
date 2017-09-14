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
