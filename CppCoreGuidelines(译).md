# C++ 核心准则(译)

中英术语对照

|   英文术语    |    译词   |
|:-------------|:----------|
|abstract      |抽象的      |
|generic       |泛型       ｜

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
By "modern C++" we mean C++ and C++14 (and soon C++17).
In other words, what would you like your code to look like in 5 year's time,
give that you can start now? In 10 years' time?
此文

The guidelines are focused on relatively higher-level issues, such as
interfaces, resource management, memory management, and concurrency.
Such rules affect application architecture and library design.
Following the rules will lead to code that is statically type safe, has no
resource leaks, and catches many more programming logic errors that is common in
code today.
And it will run fast - you can afford to do things right.

We are less concerned with low-level issues, such as naming conventions and
indentation style.
However, no topic that can help a programmer is out of bounds.
