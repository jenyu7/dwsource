
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
