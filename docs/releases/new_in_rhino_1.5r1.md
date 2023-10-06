---
title: Rhino 1.5R1
parent: Releases
nav_order: 1
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## ECMA 262 Edition 3 Conformance
Rhino 1.5 implements JavaScript 1.5, which conforms to ECMA 262 Edition 3 (sometimes referred to as "ECMAScript"). Edition 3 standardized several features of JavaScript that were present in JavaScript 1.4, including:
- regular expressions
- `switch` statements
- `do...while` loops
- statement labels and labelled `break` and `continue`
- object literals
- nested functions
- exception handling
- the `instanceof` operator
- the `in` operator

In addition, new features were added to Edition 3 and JavaScript 1.5, including:
- Perl 5 regular expressions, including operators like greedy quantifiers
- errors as exceptions
- number formatting (`Number.prototype.toFixed`, `Number.prototype.toExponential`, and `Number.prototype.toGeneral`)

#3 Changes since Rhino 1.4 Release 3
Other significant changes to Rhino since the initial release to open source (1.4 Release 3) are listed below. Bug fixes won't be mentioned here, just API changes or significant functionality changes.

### Compilation mode
Rhino has two modes of execution available. Interpretive mode has an interpreter loop implemented in Java. Compilation mode compiles JavaScript code to Java bytecodes in class files. This compilation can be done as part of script evaluation using the same APIs already available for the interpreter, or in a separate compile-time step. The code for the interpreter is located in the `org.mozilla.javascript.optimizer` package.

### JavaScript Compiler
The distribution now contains an extra class that can be invoked from the command line. This is jsc, the JavaScript compiler. This tool can be used to create Java classes from JavaScript. Options exist to allow creation of Java classes that implement arbitrary interfaces and extend arbitrary base classes, allowing JavaScript scripts to implement important protocols like applets and servlets. See [JavaScript Compiler](../../_tools/javascript_compiler.md).

### LiveConnect 3
Rhino now supports the LiveConnect 3 specification, or LC3. The most notable change is support for overloaded method resolution. See [LiveConnect Release 3 Goals/Features](https://www-archive.mozilla.org/js/liveconnect/lc3_proposal.html).

### JavaBeans properties reflected as Java properties
Java classes with getFoo/setFoo methods will have a "foo" property in the JavaScript reflection. Boolean methods are also reflected.

### Dynamic scope support
Rhino 1.5 implements support for dynamic scopes, which are particularly useful for multithreaded environments like server embeddings.

### New semantics for `ScriptableObject.defineClass`
The old rules for defining JavaScript objects using a Java class were getting baroque. Those rules are still supported, but a cleaner definition is now supported. See the [javadoc](https://javadoc.io/doc/org.mozilla/rhino/latest/org/mozilla/javascript/ScriptableObject.html#defineClass-org.mozilla.javascript.Scriptable-java.lang.Class-boolean-boolean-) for details.

### Support for the Java 2 `-jar` option
It's now possible to start the shell using the new `-jar` option in Java 2.

### Shell changes
Two changes here: addition of the "environment" and "history" top-level variables.

### Java classes visible to scripts
An attendee at JavaOne raised the point that many embeddings may not want scripts to be able to access all Java classes. This is an excellent point, and I've implemented an addition to the SecuritySupport interface that allows embedders to choose which classes are exposed to scripts.

### SecuritySupport and JavaAdapter
Andrew Wason pointed a problem with the new JavaAdapter feature (which allows JavaScript objects to implement arbitrary Java interfaces by generating class files). It didn't support the SecuritySupport interface, which allows Rhino to delegate the creation of classes from byte arrays to a routine provided by the embedding. This ability is important from a security standpoint because class creation is considered a privileged action.
I've checked in changes that fix this problem. If a SecuritySupport class is specified when a Context is created, uses of JavaAdapter will will delegate class creation to the SecuritySupport class.

### Context.exit()
Context.exit() has been changed from an instance method to a static method. This makes it match the Context.enter() method, which is also static. See the [javadoc](https://javadoc.io/doc/org.mozilla/rhino/latest/org/mozilla/javascript/Context.html#exit--) for more information on its operation.

### Context.enter(Context)
A new overloaded form of Context.enter has been added. Without the addition of this method it was not possible to attach an existing context to a thread. See the [javadoc](https://javadoc.io/doc/org.mozilla/rhino/latest/org/mozilla/javascript/Context.html#enter-org.mozilla.javascript.Context-) for more information on its operation.

### Listeners for Context
Context now supports property change listeners for a couple of its properties.
