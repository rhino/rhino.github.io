---
title: "Small Footprint"
---
# Small Footprint
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
A few changes can be made to reduce the footprint of Rhino for
embeddings where space is at a premium. On a recent build, the
length of js.jar was 603,127 bytes corresponding to 1,171,708
bytes of all uncompressed Rhino classes with debug information
included. With various changes js.jar size can be reduced to
204,689 bytes corresponding to 424,774 bytes of uncompressed
classes.

## Tools

Most embeddings won't need any of the classes in
`org.mozilla.javascript.tools` or any of its sub-packages.

## Optimizer

It is possible to run Rhino with interpreter mode only, allowing
you to remove code for classfile generation that include all
the classes from `org.mozilla.javascript.optimizer` package.

## JavaAdapter

Implementing the JavaAdapter functionality requires the ability to
generate classes on the fly. Removing
`org.mozilla.javascript.JavaAdapter` will disable this
functionality, but Rhino will otherwise run correctly.

## Class generation library

If you do not include Optimizer or JavaAdapter, nor do you use
PolicySecurityController then you do not need Rhino library for class
file generation and you can remove all the classes from in
`org.mozilla.classfile` package.

## Regular Expressions

The package `org.mozilla.javascript.regexp` can be
removed. Rhino will continue to run, although it will not be able to
execute any regular expression matches. This change saves 47,984
bytes of class files.

## Debug information

Debug information in Rhino classes consumes about 25% of code
size and if you can live without that, you can recompile Rhino to
remove it.

## smalljs.jar

Ant build script in Rhino supports smalljar target that will generate
smalljs.jar that does not include Tools, Optimizer, JavaAdapter and
Class generation library, Regular Expressions, E4X implementataion and
deprecated files. To build such minimalist jar without debug information,
run the following command from the top directory of Rhino distribution:

```sh
ant clean
ant -Ddebug=off -Dno-regexp=true -Dno-e4x=true smalljar
```

If you omit `-Dno-regexp=true`, then the resulting
smalljs.jar will include Regular Expression support. Similarly
omitting `-Dno-e4x=true` results in smalljs.jar
that includes runtime support for E4X.
