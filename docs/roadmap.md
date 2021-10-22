---
title: Roadmap
nav_order: 2
---
# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
The following are some ideas of ways people can contribute to Rhino. If something below strikes your fancy, write to norrisboyd (at) gmail (dot) com.

## Code Modernization

### Support for changing the prototype of an object using `Object.setPrototypeOf`

Being able to change the internal [__proto__](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Object/proto) property of an object has many advantages. For example, in some cases it's necessary to return functions from constructors. This is only possible in JavaScript if we use the constructor as a factory. However since the factory returns a function it wouldn't be an instance of the constructor, and wouldn't be able to share methods on its prototype.

For more information see this [bug](https://bugs.ecmascript.org/show_bug.cgi?id=264) I submitted.

### Implement ECMAScript edition 5

This is underway, see the [tracking bug](https://bugzilla.mozilla.org/show_bug.cgi?id=489326).

### Analyze regexp differences between Rhino and Java, replace if possible

Rhino's regexp engine was developed before Java had support for regular expressions. It would be good to replace Rhino's implementation with Java's implementation which we hope will be faster and more correct.

First we need to look at the differences between the Java and ECMAScript regexp grammars. If they are identical, we can substitute easily. If they are different, we need to understand the differences and come up with a design for detecting and handling the ECMAScript-specific cases. Then we need to replace the Rhino implementation with calls to the Java implementation. See [Bug 390659](https://bugzilla.mozilla.org/show_bug.cgi?id=390659)

### Remove Rhino debugger's dependency on downloaded Swing classes

_Done!_

## Performance

### Analyze and improve benchmark performance

Analyze benchmarks and see how Rhino can improve performance.

Probably the best starting point is the [V8 benchmarks](https://v8.googlecode.com/svn/data/benchmarks/v5/run.html).

## Features
https://github.com/mozilla/rhino/issues?q=is%3Aopen+is%3Aissue+label%3Afeature+

## Bugs and enhancements
https://github.com/mozilla/rhino/issues?q=is%3Aopen+is%3Aissue+label%3Abug