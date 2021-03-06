+++
title = "JCL"
description = ""
date = 2018-06-18T12:50:02Z
aliases = []
[extra]
id = 12405
[taxonomies]
categories = []
tags = []
+++

{{language}}
[[Category:JCL]]
IBM Job Control Language

Job Control Language, commonly named JCL, refers to certain scripting languages, particularly IBM mainframe operating systems, whose role is to run a batch job.

There are two distinct IBM Job Control languages:
* DOS JCL for system DOS/360, VSE, z/VSE
*  OS JCL for system  OS/360, MVS, z/OS


Although they have syntax and design rules in common, they are quite different languages.

In the JCL, the unit is the job, which consists of one or more steps. Each step consists of the execution of a specific program.

It is possible to create JCL scripts that can be called in other JCL scripts by passing parameters if necessary. Such scripts are called procedures.

==DOS JCL==
DOS JCL parameters are positional, which makes them harder to read and write, but easier for the system to parse.

==OS JCL==
In general, the OS JCL is more flexible and easier to use than the DOS JCL.


### Basic cards

The JCL statements are called cards because the  method of providing new input to a computer system was 80-column punched cards.
The OS JCL has only three basic cards:
* the JOB card, which identifies the job and provides information related to it;
* the EXEC card, which allows each step to identify which program to call;
* the DD card that identifies the datasets (files) to use during a step.


In the following examples JCL refers only to IBM OS JCL.

==Wikipedia article==
https://en.wikipedia.org/wiki/Job_Control_Language

==See also==
https://www.ibm.com/support/knowledgecenter/zosbasics/com.ibm.zos.zjcl/zjclc_basicjclconcepts.htm
