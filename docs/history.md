---
title: History
nav_order: 4
---
# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Rhino gets its name from the animal on the cover of the [O'Reilly](https://www.ora.com/) book about JavaScript.

The Rhino project was started at Netscape in the autumn of 1997. At the time, Netscape was planning to produce a version of Navigator written entirely in Java and so it needed an implementation of JavaScript written in Java. When Netscape stopped work on "Javagator," as it was called, somehow Rhino escaped the axe (rumor had it that the executives "forgot" it existed). For a time, a couple of major companies (including Sun) licensed Rhino for use in their products and paid Netscape to do so, allowing work on Rhino to continue. Now Rhino is part of Mozilla's open-source repository.

Originally, Rhino compiled all JavaScript code to Java bytecodes in generated classfiles. This produced the best performance (often beating the C implementation of JavaScript when run on a JIT), but suffered from two faults. First, compilation time was long since generating Java bytecodes and loading the generated classes was a heavyweight process. Also, the implementation effectively leaked memory since most JVMs don't really collect unused classes or the strings that are interned as a result of loading a class file.

So in fall of 1998, Rhino added an interpretive mode. The classfile generation code was moved to an optional, dynamically-loaded package. Compilation is faster and when scripts are no longer in use they can be collected like any other Java object.

Rhino was released to mozilla.org in April 1998. Originally Rhino classfile generation had been held back from release. However the licensees of Rhino have now agreed to release all of Rhino to open source, including class file generation. Since its release to open source, Rhino has found a variety of [uses](users.html) and an increasing number of people have contributed to the code.
