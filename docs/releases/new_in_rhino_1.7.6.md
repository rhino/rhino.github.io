---
title: Rhino 1.7.6
parent: Releases
nav_order: 19
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Merged many of the outstanding pull requests in the GitHub repo.

High-level changes include the following:
- Many compatibility fixes for Date, Array, String, and others (André Bargull)
- Array.find() and findIndex() (Evgeny Shepelyuk)
- String.trimLeft() and trimRight() (Travis Ennis)
- AST and "toSource" fixes (tntim96)
- Support for V8 Error extensions, including Error.captureStackTrace (Greg Brail)
- Support for typed arrays (Greg Brail)
- Support for attaching "external data" as the indexed properties of any object (Greg Brail)

André Bargull (60):
- NativeDate: Date.length and Date.UTC.length is 7
- NativeDate: Fix bug 732779 (Date.prototype.setXXX functions don't evaluate all parameters)
- NativeDate: Date.prototype.toJSON uses [[GET]] to obtain the "toISOString" property
- add js_toISOString method to format date values in ISO-8601 Extended Format with expanded year representation if necessary
- NativeDate: Update Date.parse to support simplified ISO 8601 Extended Format [15.9.1.15]
- Fix indentation in NativeDate.java
- NativeError: Error.prototype.name and Error.prototype.message are not enumerable
- NativeError: 15.11.2.1 and 15.11.4.4 updates
- Arguments: arguments object should not have its own 'constructor' property, instead it inherits 'constructor' through its prototype
- Arguments: 'callee', 'caller' and 'length' properties can be redefined for the arguments object
- BaseFunction: Function.prototype.toString arity is 0
- BaseFunction: The 'prototype' property on function instances can be redefined
- BaseFunction: The 'arguments' property can be redefined for function instances
- NativeArray: Check [[Extensible]] flag for dense-array case in [[Put]]
- NativeArray: Remove (invalid) round-trips to ScriptRuntime when getting/setting elements
- NativeArray: Follow spec more closely for Array.isArray and Array.prototype.concat
- NativeArray: Array.prototype.{indexOf, lastIndexOf} bug fixes
- NativeArray: Array.prototype.sort bug fixes (bug 728286)
- NativeArray: Multiple changes to ensure specification algorithms are followed more closely
- TopLevel,NativeGlobal,ScriptRuntime: Add cache for native error objects
- NativeNumber: Handle case when precision is Infinity for Number.prototype.{toFixed,toExponential,toPrecision}
- NativeObject: Object.prototype.toLocaleString uses [[Get]] to retrieve 'toString' property
- NativeObject: Handle undefined arguments in Object.prototype.{hasOwnProperty,propertyIsEnumerable}
- NativeString: String.prototype.replace arity is 2 instead of 1
- NativeString: Handle undefined arguments in String.prototype.slice
- ScriptRuntime: Fix range check to follow spec in numberToString()
- ScriptRuntime: Set-up proto and parent-scope for TypeErrorThrower function
- ScriptableObject: Object.defineProperties needs to make sure to call [[Get]] exactly once for each property entry
- NativeRegExp: Handle undefined arguments in compile and exec
- NativeRegExp: Report error if a RegExp flag is used more than once
- NativeRegExp: RegExp.prototype.compile arity is 2
- NativeRegExp: RegExp.prototype.lastIndex is lazily evaluated and may be set to non-writable as well
- NativeRegExpCtor: arity of RegExp constructor is 2
- NativeRegExpCtor: RegExp.prototype.{multiline,star,input,underscore} properties can be re-defined
- RegExpImpl: Multiple changes for String.prototype.{match,search,replace,split}
- Remove obsolete test case js1_2/function/regexparg-2-n.js
- update test case doctests/arguments.doctest now that the arguments object inherits the 'constructor' property through its prototype
- NativeRegExp: Make octal escape sequences match web reality
- RegExpImpl: String.prototype.split with separator=undefined no longer treated as separator='undefined'
- Fix indentation
- Context: remove duplicate code in Context#newObject()
- Context: Use StackTraceElement API to traverse stack-trace
- NativeArray: address review comment from hns
- Updated tests files per instructions in o.m.j.tests.MozillaSuiteTest
- [Bug 783797](https://bugzilla.mozilla.org/show_bug.cgi?id=783797) Function calls across multiple global scopes are not handled properly
- Silence warnings in ClassFileWriter
- Add missing @Deprecated annotations
- Add missing @Override annotations
- Add missing generic type info to deprecatedsrc/
- Add missing generic type info to toolsrc/
- Add missing generic type info to testsrc/
- Add missing generic type info to src/
- Fix invalid JavaDoc links
- Replace StringBuffer with StringBuilder if possible
- Address review comments from hns
- Generators save and later restore the current stack when processing the 'yield' operation. Our current implementation for restoring the stack unfortunately confuses the Java classfile verifier, so at class load time a VerifierError is thrown. This happens because the verifier can no longer ensure that the proper types are placed on the stack, since the stack-state is saved in a simple Object[]. Re-ordering a few operations is only necessary so the verifier will again accept the generated class. But this is only done for generators because it creates slightly less efficient code compared to the standard case.
- Add doctest and update comments with proper bug number
- [Bug 782363](https://bugzilla.mozilla.org/show_bug.cgi?id=782363) Increment/Decrement alters const variables
- [Bug 780458](https://bugzilla.mozilla.org/show_bug.cgi?id=780458) Math.IEEEremainder makes ToInt32 slow for non-integer values (V8):
- [Bug 789277](https://bugzilla.mozilla.org/show_bug.cgi?id=789277) JSC: "missing ; after statement" message prints out for the line after the problem one

C. Scott Ananian (1):
- Don't swallow empty lines in doctest; split lines on Mac/Windows/Unix.

Edison (2):
- Add working directory support to "runCommand"
- Add working directory support to "runCommand"

Elliott Baron (1):
- Add manpage for Rhino shell.

Evgeny Shepelyuk (2):
- find and findIndex initial impl
- Improving test framework + one JUnit class = one JS suite + reporting JS stacktrace on error + load function is available in JS + separate file for JS assertions

Gregory Brail (31):
- Update versions for next iteration.
- Update README for release notes.
- Change benchmark output so we can "plot" it in Maven.
- Fix code cleanup fix that broke the Java 6 build.
- Fix benchmark output file format again.
- Re-run ID map on NativeString.
- Manually add .gitignore additions from @sghill.
- Added a bit more to the README including content from @shirishp
- Add a NOTICE with the V8 copyright message.
- Move anba's new DoubleConversion code into the package with the rest of the code derived from V8.
- Remove retrotranslator code to generate 1.4-compatible bytecode. Switch bytecode generation to Java 6.
- Remove code and build artifacts pointing to the "old E4X" implementation, based on XML Beans.
- Remove unused XML beans-based E4X implementation.
- One last vestige of XML Beans.
- Re-generate ID map on NativeArray.
- Initial checkin of typed arrays and tests from V8. Fix bad capitalization.
- Fix some integer encoding and add more test cases.
- Switch typed array tests to use Evgeny's framework for running them. Make them work only with version 1.8.
- Make typed arrays only appear in 1.8.
- Add List implementation for all native arrays.
- Add "Error" to the set of standard Error constructors that could go down the new code path to create an error.
- Complete List implementation for typed arrays. Write typed array unit tests for the List implementation.
- Do not double-initialize Error.
- Make loading of typed array classes lazy. Rename Java classes so that the names are more consistent.
- Support for V8-style stack trace support: Error.prepareStackTrace, Error.captureStackTrace, Error.stackTraceLimit And "V8" format stack traces.
- Improve efficiency of NativeError via pre-cached Method objects and reduced number of default fields.
- Make "stack" non-enumerable until generated.
- Add "setExternalArrayData" to ScriptableObject to allow array data to be stored outside the core object.
- Set default version in shell to "180".
- Add method to both get and set external array data.
- Add "initSafeStandardObjects" to create standard objects with no Java class access whatsoever.

Ievgenii.Shepeliuk (2):
- `findIndex` implementation
- more V8 compatibility

Raymond Auge (1):
- [Bug 835147](https://bugzilla.mozilla.org/show_bug.cgi?id=835147) rhino exits the JVM even when run as a subshell of another java shell

Travis Ennis (2):
- Added the Javascript 1.8 String methods trimLeft and trim Right.
- Added the Javascript 1.8 String methods trimLeft and trimRight.

sainaen (1):
- Add 'LanguageVersion' annotation. Make 1.8 default version for 'ScriptsTestsBase'

sghill (1):
- removing old .cvsignore files

tntim96 (5):
- 'undefined' pattern should be treated as empty string in RegExp constructor http://www.ecma-international.org/ecma-262/5.1/#sec-15.10.4.1 https://sourceforge.net/p/htmlunit/bugs/1599/
- [Bug 798642]( https://bugzilla.mozilla.org/show_bug.cgi?id=798642) AST 'toSource' on getter/setter mistakenly adding 'function' keyword
- [Bug 800616](https://bugzilla.mozilla.org/show_bug.cgi?id=800616) Fix AST 'toSource' for Octal and Hexadecimal literals
- Fix AST empty switch to source
- Fix compile encoding error 'unmappable character for encoding ASCII'
