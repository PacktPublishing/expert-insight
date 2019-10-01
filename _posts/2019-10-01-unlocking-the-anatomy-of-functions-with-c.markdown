---
layout: post
title:  "Unlocking the Anatomy of Functions with C"
date:   2019-10-01 17:30:00 +0530
categories: []
posted_on: GitHub Page
posted_on_url: ""
article_url: ""
---

C is a _procedural_ programming language. In C, functions act as procedures, and they are building blocks of a C program. So, it is important to know what they are, how they behave, and what happens when you enter or leave a function. In general, functions (or procedures) are analogous to ordinary variables that store algorithms instead of values. By putting variables and functions together into a new type, we can store relevant values and algorithms under the same concept. In this article, we will explore functions and discuss their properties in C.

_This article is an excerpt from the book [Extreme C](https://www.packtpub.com/programming/extreme-c?utm_source=libhunt&utm_medium=referral&utm_campaign=Outreach_PEN) by Kamran Amini. Kamran teaches you to use C’s power. Building on your existing C knowledge, you will master preprocessor directives, macros, conditional compilation, pointers, and much more. You will gain new insight into algorithm design, functions, and structures. Discover how C helps you squeeze maximum performance in critical, resource-constrained applications._

# Functions in C

In this section, we want to recap everything about a C function in a single place.

A function is a box of logic that has a name, a list of input parameters, and a list of output results. In C and many other programming languages that are influenced by C, functions return only one value. In object-oriented languages such as C++ and Java, functions (which are usually called _methods_) can also throw an exception, which is not the case in C. Functions are invoked by a function call, which is simply using the name of the function to execute its logic. A correct function call should pass all required arguments to the function and wait for its execution. Note that functions are always blocking in C. This means that the caller has to wait for the called function to finish and only then can it collect the returned result. 

Opposite to a blocking function, we can have a non-blocking function. When calling a non-blocking function, the caller doesn’t wait for the function to finish and it can continue its execution. In this scheme, there is usually a _callback_ mechanism which is triggered when the called function is finished. A non-blocking function can also be referred to as an _asynchronous function_ or simply an _async function_. Since we don’t have async functions in C, we need to implement them using multithreading solutions.

It is interesting to add that nowadays, there is a growing interest in using non-blocking functions over blocking functions. It is usually referred to as _event-oriented programming_. Non-blocking functions are centric in this programming approach, and most of the written functions are non-blocking. In event-oriented programming, actual function calls happen inside an event loop, and proper callbacks are triggered upon the occurrence of an event. Frameworks such as `libuv` and `libev` promote this way of coding, and they allow you to design your software around one or several event loops.

# Importance in design

Functions are fundamental building blocks of procedural programming. Since their official support in programming languages, they have had a huge impact on the way we write code. Using functions, we can store logic in semi-variable entities and summon them whenever and wherever they are needed. Using them, we can write specific logic only once and use it multiple times in various places.

In addition, functions allow us to hide a piece of logic from other existing logic. In other words, they introduce a level of abstraction between various logical components. To give an example, suppose that you have a function, `avg`, which calculates the average of an input array. And you have another function, `main`, which calls the function, `avg`. We say that the logic inside the `avg` function is hidden from the logic inside the `main` function.

Therefore, if you want to change the logic inside `avg`, you don’t need to change the logic inside the `main` function. That’s because the `main` function only depends on the name and the availability of the `avg` function. This is a great achievement, at least for those years when we had to use punched cards to write and execute programs. We are still using this feature in designing libraries written in C or even higher-level programming languages such as C++ and Java. 

# Stack management

If you look at the memory layout of a process running in a Unix-like operating system, you notice that all of the processes share a similar layout. For now, we want to introduce _segments_; the stack segment. The stack segment is the default memory location where all local variables, arrays, and structures are allocated from. So, when you declare a local variable in a function, it is being allocated from the stack segment. This allocation always happens on top of the stack segment.

Notice the term _stack_ in the name of the segment. It means that this segment behaves like a stack. The variables and arrays are always allocated on top of it, and those at the top are the first variables to get removed. Remember this analogy with the stack concept. We will return to this in the next paragraph.

The stack segment is also used for function calls. When you call a function, a _stack frame_ containing the return address and all of the passing arguments is put on top of the stack segment, and only then is the function logic executed. When returning from the function, the stack frame is popped out, and the instruction addressed by the return address gets executed, which should usually continue the caller function.

All local variables declared in the function body are put on top of the stack frame. So, when leaving the function, all stack variables become freed. That is why we call them local variables and that is why a function cannot access the variables in another function. This mechanism also explains why local variables are not defined before entering a function and after leaving it.

Understanding the stack segment and the way it works is crucial to writing correct and meaningful code. It also prevents common memory bugs from occurring. It is also a reminder that you cannot create any variable on the stack with any size you like. The stack is a limited portion of memory, and you could fill it up and potentially receive a _stack overflow_ error. This usually happens when we have too many function calls consuming up all the stack segment by their stack frames. This is very common when dealing with recursive functions, when a function calls itself without any break condition or limit. 

# Pass-by-value versus pass-by-reference 

In most computer programming books, there is a section dedicated to pass-by-value and pass-by-reference regarding the arguments passed to a function. Fortunately, or unfortunately, we have only pass-by-value in C. There is no reference in C, so there is no pass-by-reference either. Everything is copied into the function’s local variables, and you cannot read or modify them after leaving a function.

Despite the many examples that seem to demonstrate pass-by-reference function calls, I should say that passing by reference is an illusion in C. In the rest of this section, we want to uncover this illusion and convince you that those examples are also pass-by-value. The following example will demonstrate this:

{% highlight c %}
#include <stdio.h> 
 
void func(int a) { 
  a = 5; 
} 
 
int main(int argc, char** argv) { 
  int x = 3; 
  printf(“Before function call: %d\n”, x); 
  func(x); 
  printf(“After function call: %d\n”, x); 
  return 0; 
} 
{% endhighlight %}

<p style="text-align: center; font-size: 0.85em;">Example 1.1: An example of a pass-by-value function call</p>

It is easy to predict the output. Nothing changes about the `x` variable because it is passed by value. The following output of _example 1.1_ confirms our prediction:

{% highlight shell %}
$ gcc ExtremeC_examples_chapter1_17.c 
$ ./a.out 
Before function call: 3 
After function call: 3 
$
{% endhighlight %}

<p style="text-align: center; font-size: 0.85em;">Output of example 1.1</p>

The following example, _example 1.2_, demonstrates that passing by reference doesn’t exist in C:

{% highlight c %}
#include <stdio.h> 
 
void func(int* a) { 
  int b = 9; 
  *a = 5; 
  a = &b; 
} 
 
int main(int argc, char** argv) { 
  int x = 3; 
  int* xptr = &x; 
  printf(“Value before call: %d\n”, x); 
  printf(“Pointer before function call: %p\n”, (void*)xptr); 
  func(xptr); 
  printf(“Value after call: %d\n”, x); 
  printf(“Pointer after function call: %p\n”, (void*)xptr); 
  return 0; 
} 
{% endhighlight %}

<p style="text-align: center; font-size: 0.85em;">Example 1.2: An example of pass-by-pointer function call which differs from pass-by-reference</p>

And this is the output: 

{% highlight shell %}
$ gcc ExtremeC_examples_chapter1_18.c 
$ ./a.out 
The value before the call: 3 
Pointer before function call: 0x7ffee99a88ec 
The value after the call: 5 
Pointer after function call: 0x7ffee99a88ec 
$ 
{% endhighlight %}

<p style="text-align: center; font-size: 0.85em;">Output of example 1.2 </p>

As you see, the value of the pointer is not changed after the function call. This means that the pointer is passed as a pass-by-value argument. Dereferencing the pointer inside the `func` function has allowed accessing the variable where the pointer is pointing to. But you see that changing the value of the pointer parameter inside the function doesn’t change its counterpart argument in the caller function. During a function call in C, all arguments are passed by value and dereferencing the pointers allows the modification of the caller function’s variables.

It is worth adding that the preceding example demonstrates a pass-by-pointer example in which we pass pointers to variables instead of passing them directly. It is usually recommended to use pointers as arguments instead of passing big objects to a function but why? It is easy to guess. Copying 8 bytes of a pointer argument is much more efficient than copying hundreds of bytes of a big object.

Surprisingly, passing the pointer is not efficient in the preceding example! That’s because the `int` type is 4 bytes and copying it is more efficient than copying 8 bytes of its pointer. But this is not the case regarding structures and arrays. Since copying structures and arrays are byte-wise, and all of the bytes in them should be copied one by one, it is usually better to pass pointers instead. 

# Summary

In this article, we discussed about functions and we reviewed their syntaxes. We explored their design aspects and how they contribute to a nicely shaped procedural C program. We also explained the function call mechanism and how the arguments are passed in a function call using the stack frames.

_[Extreme C](https://www.packtpub.com/programming/extreme-c?utm_source=libhunt&utm_medium=referral&utm_campaign=Outreach_PEN)_ will help C programmers dig deep into the language and its capabilities. It will help them make the most of C’s power. 

# About the Author

Kamran Amini is an expert software architect with more than 10 years of experience in the analysis, design, development, and building large-scale, distributed enterprise software systems. His skills are not limited to a specific development platform and Kamran’s architectural solutions include a variety of technologies, patterns, and concepts based on C and C++, Java, Python, etc. His passion towards C and C++ has started since his teenage as a lead for his high school’s soccer simulation team and he’s just put it to be his main axis in the career. Recently, blockchain and cryptocurrencies have been the target of his research and interest and because of his deep knowledge about classic cryptography and PKI, working on the expansion of the future possible usages and alternative blockchains are among his interests. 
