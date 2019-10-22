---
layout: post
title:  "Understanding C# basics by Mark J. Price"
date:   2019-10-22 16:00:00 +0530
categories: []
posted_on: GitHub Page
posted_on_url: ""
article_url: ""
---

C# is a strongly-typed language. Every variable and constant has a type, as does every expression that evaluates to a value. To learn C#, you will need to create some simple applications. Let's start by looking at the basics of the grammar and vocabulary of C#. 

_This article is an excerpt from the book [C# 8.0 and .NET Core 3.0 - Modern Cross-Platform Development - Fourth Edition](https://www.packtpub.com/mobile/c-8-0-and-net-core-3-0-modern-cross-platform-development-fourth-edition?utm_source=libhunt&utm_packt=referral&utm_campaign=Outreach_PEN) by Mark J. Price. Mark follows a step-by-step approach filled with exciting projects and fascinating theory for the readers in this highly acclaimed franchise. Three high-impact sections equip the audience with all they need to build modern, cross-platform applications using C# 8.0 and .NET Core 3.0._

The grammar of C# includes statements and blocks. To document your code, you can use comments. Comments should never be the only way that you document your code. Choosing sensible names for variables and functions, writing unit tests, and creating literal documents are other ways to document your code. 

# Understanding C# grammar 

## Statements 

In English, we indicate the end of a sentence with a full stop. A sentence can be composed of multiple words and phrases, with the order of words being part of the grammar. For example, in English, we say: "the black cat." The adjective, _black_, comes before the noun, _cat_. Whereas French grammar has a different order; the adjective comes after the noun, "le chat noir." What's important to take away from this is that the order matters. 

C# indicates the end of a __statement__ with a semicolon. A statement can be composed of multiple __variables__ and __expressions__. For example, in the following statement, `totalPrice` is a variable and `subtotal + salesTax` is an expression: 

{% highlight csharp %}
var totalPrice = subtotal + salesTax;
{% endhighlight %}

The expression is made up of an operand named subtotal, an operator +, and another operand named salesTax. The order of operands and operators matters. 

## Comments 

When writing your code, you're able to add comments to explain your code using a double slash, `//`. By inserting `//` the compiler will ignore everything after the `//` until the end of the line, as shown in the following code:

{% highlight csharp %}
// sales tax must be added to the subtotal 

var totalPrice = subtotal + salesTax;
{% endhighlight %}

Visual Studio Code will add or remove the comment double slashes at the start of the currently selected line(s) if you press ___Ctrl___ + ___K___ + ___C___ to add them or ___Ctrl___ + ___K___ + ___U___ to remove them. In macOS, press ___Cmd___ instead of ___Ctrl___. 

To write a multiline comment, use `/*` at the beginning and `*/` at the end of the comment, as shown in the following code: 

{% highlight csharp %}
/* 

This is a multi-line  

comment. 

*/ 
{% endhighlight %}

## Blocks 

In English, we indicate a paragraph by starting a new line. C# indicates a __block__ of code with the use of curly brackets, `{ }`. Blocks start with a declaration to indicate what it is being defined. For example, a block can define a __namespace__, __class__, __method__, or a __statement__, something we will learn more about later. 

In your current project, note that the grammar of C# is written for you by the dotnet CLI tool. I've added some comments to the statements written by the project template, as shown in the following code: 

{% highlight csharp %}
using System; // a semicolon indicates the end of a statement 

namespace Basics 
{ 
  class Program 
  { 
    static void Main(string[] args) 

    { // the start of a block 

      Console.WriteLine("Hello World!"); // a statement 

    } // the end of a block 
  } 
}
{% endhighlight %}

# Understanding C# vocabulary 

The C# vocabulary is made up of __keywords__, __symbol characters__, and __types__. 

Some of the predefined, reserved keywords that you will commonly see include `using`, `namespace`, `class`, `static`, `int`, `string`, `double`, `bool`, `if`, `switch`, `break`, `while`, `do`, `for`, and `foreach`. 

Some of the symbol characters that you will see include `"`, `'`, `+`, `-`, `*`, `/`, `%`, `@`, and `$`. 

By default, Visual Studio Code shows C# keywords in blue in order to make them easier to differentiate from other code. Visual Studio Code allows you to customize the color scheme. 

1. In Visual Studio Code, navigate to __Code__ \| __Preferences__ \| __Color Theme__ (it is on the __File__ menu on Windows), or press ___Ctrl___ or ___Cmd___ + ___K___, ___Ctrl___ or ___Cmd___ + ___T___. 

2. Select a color theme.

There are other contextual keywords that only have a special meaning in a specific context. However, that still means that there are only about 100 actual C# keywords in the language. The English language has more than 250,000 distinct words, so how does C# get away with only having about one hundred keywords? Moreover, why is C# so difficult to learn if it has only 0.0416% of the amount of words compared to the English language? 

One of the key differences between a human language and a programming language is that developers need to be able to define the new "words" with new meanings. Apart from the 104 keywords in the C# language, this book will teach you about some of the hundreds of thousands of "words" that other developers have defined, but you will also learn how to define your own "words." 

## Help for writing correct code 

Plain text editors such as Notepad don't help you write correct English. Likewise, Notepad won't help you write correct C# either. 

Microsoft Word can help you write English by highlighting spelling mistakes with red squiggles, with Word saying that "icecream" should be ice-cream or ice cream, and grammatical errors with blue squiggles, like a sentence should have an uppercase first letter. 

Similarly, Visual Studio Code's C# extension helps you write C# code by highlighting spelling mistakes, like the method name should be `WriteLine` with an uppercase L, and grammatical errors, like statements that must end with a semicolon. 

The C# extension constantly watches what you type and gives you feedback by highlighting problems with colored squiggly lines, similar to that of Microsoft Word. 

## Verbs are methods 

In English, verbs are doing or action words, like run and jump. In C#, doing or action words are called __methods__. There are hundreds of thousands of methods available to C#. In English, verbs change how they are written based on when in time the action happens. For example, Amir was _jumping_ in the past, Beth _jumps_ in the present, they _jumped_ in the past, and Charlie will _jump_ in the future. 

In C#, methods such as `WriteLine` change how they are called or executed based on the specifics of the action. This is called __overloading__. Consider the following example: 

{% highlight csharp %}
// outputs a carriage-return  

Console.WriteLine(); 

// outputs the greeting and a carriage-return Console.WriteLine("Hello Ahmed"); 

// outputs a formatted number and date and a carriage-return Console.WriteLine( 

  "Temperature on {0:D} is {1}°C.", DateTime.Today, 23.4);
{% endhighlight %}

A different analogy is that some words are spelled the same, but have different meanings depending on the context. 

## Nouns are types, fields, and variables 

In English, nouns are names that refer to things. For example, Fido is the name of a dog. The word "dog" tells us the type of thing that Fido is, and so in order for Fido to fetch a ball, we would use his name. 

In C#, their equivalents are __types__, __fields__, and __variables__. For example,  `Animal` and `Car` are types; that is, they are nouns for categorizing things. `Head` and `Engine` are fields, that is, nouns that belong to `Animal` and `Car`. Whilst `Fido` and `Bob` are variables, that is, nouns for referring to a specific thing. 

There are tens of thousands of types available to C#, though have you noticed how I didn't say, "There are tens of thousands of types in C#?" The difference is subtle but important. The language of C# only has a few keywords for types, such as `string` and `int`, and strictly speaking, C# doesn't define any types. Keywords such as `string` that look like types are __aliases__, which represent types provided by the platform on which C# runs. 

It's important to know that C# cannot exist alone; after all, it's a language that runs on variants of .NET. In theory, someone could write a compiler for C# that uses a different platform, with different underlying types. In practice, the platform for C# is .NET, which provides tens of thousands of types to C#, including `System.Int32`, which is the C# keyword alias `int` maps to, as well as many more complex types, such as `System.Xml.Linq.XDocument`.

It's worth taking note that the term __type__ is often confused with __class__. Have you ever played the parlor game, _Twenty Questions_, also known as _Animal, Vegetable, or Mineral_? In the game, everything can be categorized as an animal, vegetable, or mineral. In C#, every __type__ can be categorized as a `class`, `struct`, `enum`, `interface`, or `delegate`. The C# keyword `string` is a `class`, but `int` is a `struct`. So, it is best to use the term __type__ to refer to both. 

# Summary 

_To gain a solid foundation with C# 8.0 and .NET Core 3.0, refer to our latest book [C# 8.0 and .NET Core 3.0 - Modern Cross-Platform Development - Fourth Edition](https://www.amazon.com/8-0-NET-Core-3-0-Cross-Platform/dp/1788478126?utm_source=libhunt&utm_packt=referral&utm_campaign=Outreach_PEN) by Mark J. Price.The fourth edition is updated with new chapters on Content Management Systems (CMS) and machine learning with ML.NET, and it dives deep into the Visual Studio Code editor that works across all operating systems._

_Dive deep into the Visual Studio Code editor that works across all operating systems, and the fourth edition is updated with new chapters on Content Management Systems (CMS) and machine learning with ML.NET. To gain a solid foundation with C# 8.0 and .NET Core 3.0, refer to our latest book [C# 8.0 and .NET Core 3.0 - Modern Cross-Platform Development - Fourth Edition](https://www.amazon.com/8-0-NET-Core-3-0-Cross-Platform/dp/1788478126?utm_source=libhunt&utm_packt=referral&utm_campaign=Outreach_PEN) by Mark J. Price._

# About the Author  

Mark J. Price is a Microsoft Specialist: Programming in C# and Architecting Microsoft Azure Solutions, with more than 20 years of educational and programming experience. Since 1993, Mark has passed more than 80 Microsoft programming exams and specializes in preparing others to pass them too. His students range from professionals with decades of experience to 16-year-old apprentices with none. He successfully guides all of them by combining educational skills with real-world experience in consulting and developing systems for enterprises worldwide. 

Between 2001 and 2003, Mark was employed full-time to write official courseware for Microsoft in Redmond, USA. His team wrote the first training courses for C# while it was still an early alpha version. While with Microsoft, he taught "train-the-trainer" classes to get other MCTs up-to-speed on C# and .NET. Currently, Mark creates and delivers training courses for Episerver's Digital Experience Cloud, the best .NET CMS for Digital Marketing and E-commerce. In 2010, Mark studied for a Postgraduate Certificate in Education (PGCE). He taught GCSE and A-Level mathematics in two London secondary schools. He holds a Computer Science BSc. Hons. Degree from the University of Bristol, UK. 

 

 
