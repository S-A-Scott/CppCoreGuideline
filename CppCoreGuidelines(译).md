# C++ 核心准则(译)

中英术语对照

|   英文术语    |    译词         |
|:-------------|:----------------|
|abstract      |抽象的            |
|generic       |泛型              |
|hierarchy     |继承体系(层次结构)  |
|philosophy    |哲学              |


1. 涉及C++ 语言关键字的相关术语保留。例如C++,class,public,private,namespace ......
2. 用中文难以表达原意的词保留。

2015年10月10日

作者:

* [Bjarne Stroustrup](http://www.stroustrup.com)
* [Herb Sutter](http://herbsutter.com/)

你可以阅读本指南范围和结构的说明，或是转至以下内容

* [P: 哲学](#S-philosophy)
* [I: 接口](#S-interfaces)
* [F: 函数](#S-functions)
* [C: 类和类的层次结构](#S-class)
* [Enum: 枚举](#S-enum)
* [ES: 表达式和声明](#S-expr)
* [E: 错误处理](#S-errors)
* [R: 资源管理](#S-resource)
* [T: 模版和泛型编程](#S-templates)
* [CP: 并发](#S-concurrency)
* [SL: 标准库](#S-stdlib)
* [SF: 源文件](#S-source)
* [CPL: C风格编程](#S-cpl)
* [PRO: Profiles](#S-profile)
* [GSL: Guideline support library](#S-gsl)
* [FAQ: Answers to frequently asked questions](#S-faq)

Supporting sections:

* [NL: Naming and layout](#S-naming)
* [PER: Performance](#S-performance)
* [N: Non-Rules and myths](#S-not)
* [RF: Refrences](S-references)
* [Appendix A: Libraries](S-libraries)
* [Appendix B: Modernizing code](#S-modernizing)
* [Appendix C: Discussion](#S-discussion)
* [Glossary](#S-glossary)
* [To-do: Unclassified proto-rules](#S-unclassified)

or look at a specific language feature

* [assignment](#S-???)
* [`class`](#S-class)
* [constructor](#SS-ctor)
* [derived `class`](#SS-hier)
* [destructor](#SS-ctor)
* [exception](#S-errors)
* [`for`](#S-???)
* [`inline`](#S-class)
* [initialization](#S-???)
* [lambda expression](#SS-lambdas)
* [operator](#S-???)
* [`public`, `private`, and `protected`](#S-???)
* [`static_assert`](#S-???)
* [`struct`](#S-class)
* [`template`](#S-???)
* [`unsigned`](#S-???)
* [`virtual`](#SS-hier)

Definitions of terms used to express and discuss the rules, that are not
language-technical, but refer to design and programming techniques

* error
* exception
* failure
* invariant
* leak
* precondition
* postcondition
* resource
* exception guarantee

# <a name="S-abstract"></a> 摘要

This document is a set of guidelines for using C++ well.
The aim of this document is to help people to use modern C++ effectively.
By "modern C++" we mean C++11 and C++14 (and soon C++17).
In other words, what would you like your code to look like in 5 year's time,
give that you can start now? In 10 years' time?
本文由一系列让人们更好使用C++ 的指南构成，这些指南旨在帮助人们更高效的
使用现代C++技术。这里所说的现代C++是指C++11 和 C++ 14(以及不久之后的C++17). 
换句话说，在接下来的5年内，你希望能写出怎样的代码？ 10年内呢？

The guidelines are focused on relatively higher-level issues, such as
interfaces, resource management, memory management, and concurrency.
Such rules affect application architecture and library design.
Following the rules will lead to code that is statically type safe, has no
resource leaks, and catches many more programming logic errors that is common in
code today.
And it will run fast - you can afford to do things right.
这篇指南着眼于相对高层的问题，例如接口，资源管理，内存管理，以及并发性。
这些规则影响着应用的体系结构和库的设计。

We are less concerned with low-level issues, such as naming conventions and
indentation style.
However, no topic that can help a programmer is out of bounds.
