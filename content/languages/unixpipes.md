+++
title = "UnixPipes"
description = ""
date = 2011-11-01T16:28:08Z
aliases = []
[extra]
id = 2798
[taxonomies]
categories = []
tags = []
+++

{{language
|hopl=no
}}
''UnixPipes is really the same language as [[:Category:UNIX Shell|UNIX Shell]].''

'''Unix Pipes''' is a collection of tools which doesn't use any Turing complete sublanguages. The idea of the system is to solve programming problems using only the pipelines alone. The tools are not restricted to the commonly available tools in [[UNIX]]. Any new tool is allowed as long as it is sharp enough. (i.e does one and only one thing very well).

If a new tool is introduced, a description of the tool is required.

Using utilities from, [http://packages.debian.org/unstable/utils/moreutils moreutils]

'''unfold'''

Defining unfold as the opposite of xargs, i.e take a list of arguments and send them one at a time.
The definition would be

```bash

|cat unfold
num=$1
while read xxx; do
    for i in $xxx; do
        echo $i
    done |xargs -n $num echo
done

|echo 1 2 3 4 5 6 7 8 |unfold 3
1 2 3
4 5 6
7 8


```


== Deleted solutions ==
We delete a UnixPipes solution when it is too similar to its UNIX Shell equivalent, or when it is incorrect (but the UNIX Shell solution is correct).

# [[Hello world/Standard error]] -- Merged to UNIX Shell.
# [[Sieve of Eratosthenes]] -- Deleted for being incorrect.
# [[Sockets]] -- Merged to UNIX Shell.
# [[String case]] -- Merged to UNIX Shell.
