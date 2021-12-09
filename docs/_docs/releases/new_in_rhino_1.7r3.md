---
title: Rhino 1.7R3
parent: Releases
nav_order: -16
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
### ECMAScript 5 support

ECMAScript 5 support was added to Rhino by Raphael Speyer during a Google Summer of Code project mentored by Norris Boyd. Rhino 1.7R3 supports most of ES5 except for Strict Mode.

### JavaScript 1.8 support

Rhino 1.7R3 has partial support for [JavaScript 1.8](https://web.archive.org/web/20210502042346mp_/https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.8) contributed by Hannes Wallnöfer and Andreas Bolka. This includes expression closures and destructuring assignment shorthand but not generator expressions.

Note that JavaScript 1.8 features have to be enabled explicitly by selecting language version `180` in the shell, or `Context.VERSION_1_8` in embedded mode.

### New AST API

Steve Yegge has contributed a new AST API to Rhino which should be useful for people building JavaScript specific tools. The AST classes are in the `org.mozilla.javascript.ast` package.

### CommonJS module support

A fully compliant [CommonJS module implementation](http://wiki.commonjs.org/wiki/Modules/1.1.1) was contributed by Attila Szegedi. CommonJS modules are also available in the Rhino shell using the `-modules`, `-main`, and `-sandbox` command line options.

### JS Objects implement Java collections

JavaScript Objects now implement the `java.util.Map` interface while Arrays implement `java.util.List`. This means that JavaScript objects can be passed seamlessly to Java methods expecting a Map while arrays can be passed to methods expecting a List or java.util.Collection.

### JSDoc comment parsing

The Rhino parser is now capable of recognizing JSDoc-like comments (starting with `/**`). This feature is disabled by default and has to be enabled by setting the corresponding flag in the `CompilerEnviron` object.

### Performance improvements

Rhino has seen some performance improvements since the last release which are most notable when running benchmarks or the test suite.