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

It is interesting to add that nowadays, there is a growing interest in using non-blocking functions over blocking functions. It is usually referred to as event-oriented programming. Non-blocking functions are centric in this programming approach, and most of the written functions are non-blocking. In event-oriented programming, actual function calls happen inside an event loop, and proper callbacks are triggered upon the occurrence of an event. Frameworks such as libuv and libev promote this way of coding, and they allow you to design your software around one or several event loops. 
