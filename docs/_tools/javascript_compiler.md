---
title: "JavaScript compiler"
---
# JavaScript compiler
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
### Overview

The JavaScript compiler translates JavaScript source into Java class files. The resulting Java class files can then be loaded and executed at another time, providing a convenient method for transferring JavaScript, and for avoiding translation cost.

Note that the top-level functions available to the shell (such as print) are not available to compiled scripts when they are run outside the shell.

### Compiler command line

`java org.mozilla.javascript.tools.jsc.Main` [_options_] `file1.js [file2.js...]`

where _options_ are:

`-extends` _java-class-name_

Specifies that a java class extending the Java class _java-class-name_ should be generated from the incoming JavaScript source file. Each global function in the source file is made a method of the generated class, overriding any methods in the base class by the same name.

`-implements` _java-intf-name_

Specifies that a java class implementing the Java interface _java-intf-name_ should be generated from the incoming JavaScript source file. Each global function in the source file is made a method of the generated class, implementing any methods in the interface by the same name.

`-debug

 -g`

Specifies that debug information should be generated. May not be combined with optimization at an optLevel greater than zero.

`-main-method-class` _className_

Specify the class name used for main method implementation. The class must have a method matching `public static void main(Script sc, String[] args)`.

`-nosource`

Does not save the source in the class file. Functions and scripts compiled this way cannot be decompiled. This option can be used to avoid distributing source or simply to save space in the resulting class file.

`-o` _outputFile_

Writes the class file to _outputFile_, which should end in .class and must be a writable filename.

`-d` _outputDirectory_

Writes the class file to _outputDirectory_.

`-opt` _optLevel_

Optimizes at level _optLevel_, which must be an integer between -1 and 9. See [Optimization](../_docs/optimization.md) for more details. If _optLevel_ is greater than zero, `-debug` may not be specified.

`-package` _packageName_

Specifies the package to generate the class into. The string _packageName_ must be composed of valid identifier characters optionally separated by periods.

`-version` _versionNumber_

Specifies the language version to compile with. The string _versionNumber_ must be one of 100, 110, 120, 130, 140, 150, 160, or 170. See [JavaScript Language Versions](../_docs/overview.md#javascript_language_versions) for more information on language versions.

### Examples

```
$ cat test.js
java.lang.System.out.println("hi, mom!");
$ java org.mozilla.javascript.tools.jsc.Main test.js
$ ls *.class
test.class
$ java test
hi, mom!
$ java org.mozilla.javascript.tools.jsc.Main -extends java.applet.Applet
    -implements java.lang.Runnable NervousText.js
```

---

--[Norrisboyd](/user:norrisboyd) 12:26, 13 June 2007 (PDT)