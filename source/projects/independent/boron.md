# The Boron Language

~

When I was about twelve years old, I saw in Barnes & Noble a book about how to code.  Fascinated, I asked my mother if we could buy it.  Knowing my interest in all things technical, my mother permitted me.  Opening the book, I learned about the Python programming language and some of its basic features.

I read through the exercises contained in the book and quickly taught myself Python.  Little did I know that I would be using it in my college computer science class years later.

From the beginning, I was fascinated by Python's elegant, simple, and readable syntax.  I always wondered if it was possible for me to develop my own computer language... but as a young boy I knew nothing of the great effort involved in developing and maintaining a programming language.

Six years later, after much Internet research and time spent at my laptop, I successfully developed my first programming language: Boron.

## Design Philosophy

Boron was designed to be easy to read and fast.  Furthermore, I was not and am not very knowledgeable about low-level compiler functionality, and I didn't want to embark on the journey of using LLVM or another compiler toolkit.

Based on my working knowledge of C, I designed the Boron compiler to output raw C that would then be compiled a second time by _GCC_ or another C language compiler.

## Current Features

Boron currently supports variable definition, loops, functions, and structs.

## Planned Improvements

My academic work and extracurricular obligations keep me pretty busy, so the Boron language is not currently under active development and no improvements are planned in the near future.

However, future improvements to Boron may include the expansion of its object-oriented capabilities as well as LLVM support.

## Source Code

The Boron compiler is completely open-source and licensed under the MIT License.  Its source code is available on GitHub.

[https://github.com/josephrhobbs/boron](https://github.com/josephrhobbs/boron)