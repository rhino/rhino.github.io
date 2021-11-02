---
title: Overview
---
# {{ page.title }}

{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents

{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Introduction

Most people who have used [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) before have done so by adding scripts to their [HTML](https://developer.mozilla.org/en-US/docs/Glossary/HTML) web pages. However, Rhino is an implementation of the core language only and doesn't contain objects or methods for manipulating HTML documents.

Rhino contains

- All the features of [JavaScript 1.7](https://web.archive.org/web/20210502042346mp_/https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.7)
- Allows direct scripting of Java
- [A JavaScript shell](../_tools/shell.md) for executing JavaScript scripts
- [A JavaScript compiler](../_tools/javascript_compiler.md) to transform JavaScript source files into Java class files
- [A JavaScript debugger](../_tools/debugger.md) for scripts executed with Rhino

## Language

The JavaScript language itself is standardized by [Standard ECMA-262 ECMAScript: A general purpose, cross-platform programming language](https://www.ecma-international.org/publications/standards/Ecma-262.htm). Rhino 1.3 and greater conform to Edition 3 of the Standard.

Rhino 1.6 and greater implement [ECMA-357 ECMAScript for XML (E4X)](https://web.archive.org/web/20131104082608/http://www.ecma-international.org/publications/standards/Ecma-357.htm). See the specification for more information on the standard, and [Rhino version 1.6R1 release notes](https://www-archive.mozilla.org/rhino/rhino16r1) for details on the implementation in Rhino.

In addition, Rhino has implemented JavaAdapters, which allows JavaScript to implement any Java interface or extend any Java class with a JavaScript object. See the `enum.js` example for more information.

Numerous books and tutorials on JavaScript are available. [JavaScript: The Definitive Guide](https://www.oreilly.com/catalog/jscript5/) is recommended, and contains a chapter on Rhino.

## Internationalization

The messages reported by the JavaScript engine are by default retrieved from the property file `org/mozilla/javascript/resources/Messages.properties`. If other properties files with extensions corresponding to the current locale exist, they will be used instead.

## JavaScript Language Versions

Some behavior in the JavaScript engine is dependent on the language version. In browser embeddings, this language version is selected using the `LANGUAGE` attribute of the `SCRIPT` tag with values such as `"JavaScript1.2"`.

## Security

The security features in Rhino provide the ability to track the origin of a piece of code (and any pieces of code that it may in turn generate). These features allow for the implementation of a traditional URL-based security policy for JavaScript as in Netscape Navigator. Embeddings that trust the JavaScript code they execute may ignore the security features.

Embeddings that run untrusted JavaScript code must do two things to enable the security features. First, every `Context` that is created must be supplied an instance of an object that implements the `SecuritySupport` interface. This will provide Rhino the support functionality it needs to perform security-related tasks.

Second, the value of the property `security.requireSecurityDomain` should be changed to `true` in the resource bundle `org.mozilla.javascript.resources.Security`. The value of this property can be determined at runtime by calling the `isSecurityDomainRequired` method of `Context`. Setting this property to `true` requires that any calls that compile or evaluate JavaScript must supply a security domain object of any object type that will be used to identify JavaScript code. In a typical client embedding, this object might be a string with the URL of the server that supplied the script, or an object that contains a representation of the signers of a piece of code for certificate-based security policies.

When JavaScript code attempts a restricted action, the security domain can be retrieved in the following manner. The class context should be obtained from the security manager (see `java.lang.SecurityManager.getClassContext()`). Then, the class of the code that called to request the restricted action can be obtained by looking an appropriate index into the class context array. If the caller is JavaScript the class obtained may be one of two types. First, it may be the class of the interpreter if interpretive mode is in effect. Second, it may be a generated class if classfile generation is supported. An embedding can distinguish the two cases by calling `isInterpreterClass()` in the `Context` class. If it is the interpreter class, call the `getInterpreterSecurityDomain()` method of `Context` to obtain the security domain of the currently executing interpreted script or function. Otherwise, it must be a generated class, and an embedding can call `getSecurityDomain()` in the class implementing `SecuritySupport`. When the class was defined and loaded, the appropriate security domain was associated with it, and can be retrieved by calling this method. Once the security domain has been determined, an embedding can perform whatever checks are appropriate to determine whether access should be allowed.
