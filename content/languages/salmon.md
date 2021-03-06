+++
title = "Salmon"
description = ""
date = 2011-11-05T01:53:42Z
aliases = []
[extra]
id = 10783
[taxonomies]
categories = []
tags = []
+++

{{language|Salmon
|site=http://salmonpl.net/
|LCT=no
}}

Salmon is a general-purpose, multi-paradigm language that supports imperative, object-oriented, and functional programming styles, among others.  It supports writing code at either a high level or a low level, and intermixing the two.  Salmon is designed to support the full range of programming tasks, from quick and simple scripts to large, multi-developer software projects, with strong support for modularity.  It is designed to support interpretation or compilation, with the ability to specify low-level details where needed to optimize compiled code.  Readability and maintainability of code are a priority with Salmon.

Salmon has a powerful, flexible, strong type system.  The programmer is allowed to leave off all explicit type information, as in a traditional dynamically-typed language.  The programmer may also put in full static type information, allowing a compiler to do full static type checking and generate code that does not have to do any dynamic type checking or dispatch at run time.  Or the programmer may put in type information in some places but not others.  A Salmon program may gradually evolve from an initial, quick prototype with no type information specified to a more mature system with detailed type information.

The Salmon type system also allows an unusual degree of freedom in expressing types.  For example, the user may specify a given variable has a value that is an integer in either of the ranges 0 - 15 or 20 - 25.  Or the user may specify a variable may be any string matching a given regular expression.  Types can also be specified that won't be known until run time, and types are first-class values in Salmon, allowing them to be passed into functions, stored in data structures, and created on the fly.

Memory management in Salmon may either be explicit or implicit, or a mixture of the two.  The programmer may do explicit memory management either by specifying finite lifetimes for scoped variables and other declarations that implicitly end when the scope does (stack lifetimes) or by explicitly calling a delete() procedure to end the lifetimes of indefinite-lifetime entities (heap lifetimes).  Or the programmer may let automatic garbage collection de-allocate things that are no longer needed.  Even when the programmer explicitly de-allocates entities, safety is maintained -- trying to use a reference to an entity that no longer exists always results in an exception that can be caught and handled rather than undefined behavior.

Other unusual features of Salmon include support for modules adding private data to datastructures shared with other modules and a theorem/proof system to allow the compiler to check the reasoning of the programmer about virtually any property, though the current implementation of Salmon does not yet support checking such proofs.

Salmon currently has a full implementation in the form of a portable interpreter written in C, and a detailed reference manual specifying the language.  A plug-in mechanism in the interpreter allows native code modules to be dynamically loaded and called from Salmon, allowing code written in C or any other compiled language to be called from Salmon.

The Salmon interpreter and documentation are all in the public domain.
