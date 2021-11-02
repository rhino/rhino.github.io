---
title: "Examples"
---

# Examples

{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents

{: .no_toc .text-delta }

1. TOC
{:toc}

---
Examples have been provided that show how to control the JavaScript engine and how  to implement scriptable host objects. All the examples are in the git tree at [mozilla/js/rhino/examples](https://github.com/mozilla/rhino/tree/master/examples/).

## Sample Scripts

The [unique.js](https://github.com/mozilla/rhino/tree/master/examples/unique.js) script allows printing unique lines from a file.

The [liveConnect.js](https://github.com/mozilla/rhino/tree/master/examples/liveConnect.js) script shows a sample usage of LiveConnect (Java-to-JavaScript connectivity).

The [jsdoc.js](https://github.com/mozilla/rhino/tree/master/examples/jsdoc.js) script is a JavaScript analog to Java's `javadoc`. It makes heavy use of regular expressions.

The [checkParam.js](https://github.com/mozilla/rhino/tree/master/examples/checkParam.js) script is a useful tool to check that `@param` tags in Java documentation comments match the parameters in the corresponding Java method.

The [enum.js](https://github.com/mozilla/rhino/tree/master/examples/enum.js) script is a good example of using a JavaAdapter to implement a Java interface using a JavaScript object.

The [NervousText.js](https://github.com/mozilla/rhino/tree/master/examples/NervousText.js) script is a JavaScript implementation of the famous NervousText applet using JavaScript compiled to Java classes using [jsc](../_tools/javascript_compiler.md). It can be run in the HTML page [NervousText.html](https://github.com/mozilla/rhino/tree/master/examples/NervousText.html).

## Controlling the JavaScript Engine

### The RunScript class

[RunScript.java](https://github.com/mozilla/rhino/tree/master/examples/RunScript.java) is a simple program that executes a script from the command line.

### The Control class

[Control.java](https://github.com/mozilla/rhino/tree/master/examples/Control.java) is a program that executes a simple script and then manipulates the result.

### JavaScript Shell

[Shell.java](https://github.com/mozilla/rhino/tree/master/examples/Shell.java) is a program that executes JavaScript programs; it is a simplified version of the shell in the `tools` package. The programs may be specified as files on the command line or by typing interactively while the shell is running.

### PrimitiveWrapFactory

[PrimitiveWrapFactory.java](https://github.com/mozilla/rhino/tree/master/examples/PrimitiveWrapFactory.java) is an example of a WrapFactory that can be used to control the wrapping behavior of the Rhino engine on calls to Java methods.

### Multithreaded Script Execution

[DynamicScopes.java](https://github.com/mozilla/rhino/tree/master/examples/DynamicScopes.java) is a program that creates a single global scope object and then shares it across multiple threads. Sharing the global scope allows both information to be shared across threads, and amortizes the cost of Context.initStandardObjects by only performing that expensive operation once.

## Implementing Host Objects

First check out the [tutorial](../_tutorials/embedding_tutorial.md) if you haven't already.

### The Foo class - Extending ScriptableObject

[Foo.java](https://github.com/mozilla/rhino/tree/master/examples/Foo.java) is a simple JavaScript host object that includes a property with an associated action and a variable argument method.

### The Matrix class - Implementing Scriptable

[Matrix.java](https://github.com/mozilla/rhino/tree/master/examples/Matrix.java) provides a simple multidimensional array by implementing the Scriptable interface.

### The File class - An advanced example

[File.java](https://github.com/mozilla/rhino/tree/master/examples/File.java) extends ScriptableObject to provide a means of reading and writing files from JavaScript. A more involved example of host object definition.
