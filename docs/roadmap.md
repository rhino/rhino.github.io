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

### Analyze regexp differences between Rhino and Java, replace if possible

Rhino's regexp engine was developed before Java had support for regular expressions. It would be good to replace Rhino's implementation with Java's implementation which we hope will be faster and more correct.

First we need to look at the differences between the Java and ECMAScript regexp grammars. If they are identical, we can substitute easily. If they are different, we need to understand the differences and come up with a design for detecting and handling the ECMAScript-specific cases. Then we need to replace the Rhino implementation with calls to the Java implementation. See [Bug 390659](https://bugzilla.mozilla.org/show_bug.cgi?id=390659)

## Performance

### Analyze and improve benchmark performance

Analyze benchmarks and see how Rhino can improve performance.

Probably the best starting point is the [V8 benchmarks](https://v8.googlecode.com/svn/data/benchmarks/v5/run.html).

## Features
https://github.com/mozilla/rhino/issues?q=is%3Aopen+is%3Aissue+label%3Afeature+

## Bugs and enhancements
https://github.com/mozilla/rhino/issues?q=is%3Aopen+is%3Aissue+label%3Abug