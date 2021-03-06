+++
title = "Mirah"
description = ""
date = 2011-09-20T01:21:38Z
aliases = []
[extra]
id = 10411
[taxonomies]
categories = []
tags = []
+++

{{language
|tags=mirah
|express=implicit
|strength=strong
|checking=static
|site=http://www.mirah.org/}}
Mirah is a new way of looking at [[runs on vm::JVM]] languages. In attempting to build a replacement for [[Java]], we have followed a few guiding principals:
* No runtime library
Mirah does not impose any jar files upon you. YOU decide what your application's dependencies should be.
* Clean, simple syntax
We have borrowed heavily from [[derived from::Ruby]], but added static typing and minor syntax changes to support the JVM's type system. The result is pleasing to the eye, but as powerful as Java.
* [[Metaprogramming]] and macros
Mirah supports various mechanisms for compile-time metaprogramming and macros. Much of the "open class" feel of dynamic languages is possible in Mirah.
* No performance penalty
Because Mirah directly targets the JVM's type system and JVM [[bytecode]], it performs exactly as well as Java.
