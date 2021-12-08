---
title: New in Rhino 1.5R4
parent: Releases
nav_order: -4
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
This is a log of changes since the release of Rhino 1.5 Release 3.

## Rhino debug API changes
A new, incompatible Rhino debug API gives an option to monitor entering/leaving of script functions while decreasing the amount of code to implement the API in the Rhino core. Details are available [here](1.5r3_debug_api_changes.md). With the new API [Rhino Debugger](../../_tools/debugger.md) provides options to break on function enter/exit, can debug scripts defined by eval and Function construction and scripts loaded prior the debugger were started.

## WrapFactory introduced, WrapHandler deprecated
A design flaw in the WrapHandler interface (a call to a Java contructor from JavaScript would result in a call to wrap the result, which would then be cast to a Scriptable) inspired the deprecation of that interface and the introduction of a new class, WrapFactory, that contains a new method called on the result of a constructor call and can be customized by application if necessary.
In addition, WrapFactory has the new `setJavaPrimitiveWrap` method to control if instances of Java `String` and `Number` class should be wrapped to special script objects as any other Java objects so a script can access any method `String` and `Number`, or they should be converted to JavaScript primitive strings and numbers.

## New security interfaces
Igor Bukanov contributed a new security implementation that allows integration with Java2 security model and prevents scripts to escape the security sandbox via eval/Function schemes.

Due to this changes SecuritySupport interface is replaced by ClassShutter and SecurityController, where ClassShutter controls which classes are visible to scripts via LiveConnect and SecurityController provides permission management. For compatibility SecuritySupport is still available as a deprecated interface but only its visibleToScripts method is used as an alias for ClassShutter.visibleToScripts. See API documentation for new classes for details.

An implementation of SecurityController that uses java policy settings to restrict script permissions based on its URL is available with Rhino shell. See the [JavaPolicySecurity](/rhino/javadoc/org/mozilla/javascript/tools/shell/JavaPolicySecurity.html) source for details. To activate it, set the `rhino.use_java_policy_security` system property to true when invoking Rhino shell together with installing a security manager.

## Serialization changes
Due to changes in Rhino implementation and bug fixes in serialization support runtime data serialized in Rhino 1.5 Release 3 can not be read back in the Release 4.

## Regular expressions improvements
Roger Lawrence provided new regular expressions implementation which fully confirms to EcmaScript 262 standard and faster.

## Scripting of classes from any class loader
Christopher Oliver contributed code to allow to use the `Packages` object as a constructor taking a class loader argument so a script can access classes defined by that class loader. For example, to access classes from foo.jar file in the current directory, the following can be used:
```js
// create class loader
var loader = new java.net.URLClassLoader([new java.net.URL("file:./foo.jar")]);
// create its LiveConnect wrapper
var fooJar = new Packages(loader);
// create an instance of the class For from foo.jar
var obj = new fooJar.Foo(1, 2, 3);
obj.someMethod();
```

## Shell function to run external processes.
A new `runCommand` function is added to [Rhino Shell](../../_tools/shell.md) to run external priocesses. For details, see [runCommand](/rhino/javadoc/org/mozilla/javascript/tools/shell/Global.html#runCommand-org.mozilla.javascript.Context-org.mozilla.javascript.Scriptable-java.lang.Object:A-org.mozilla.javascript.Function-)

## Resolved Bugzilla reports
The following Rhino reports in Bugzilla where resolved for Rhino 1.5 Release 4.
- [61579](http://bugzilla.mozilla.org/show_bug.cgi?id=61579) context.decompileScript doesn't work.
- [72021](http://bugzilla.mozilla.org/show_bug.cgi?id=72021) The ScriptRuntime class tries to convert even the String values to JavaNativeObject
- [83051](http://bugzilla.mozilla.org/show_bug.cgi?id=83051) A function defined under a with block can't be invoked outside it
- [104089](http://bugzilla.mozilla.org/show_bug.cgi?id=104089) Cannot reattach context to its thread because of the bug in Context class
- [105438](http://bugzilla.mozilla.org/show_bug.cgi?id=105438) SourceName and lineNumbers of syntax errors in Javascript files not dispalyed.
- [106548](http://bugzilla.mozilla.org/show_bug.cgi?id=106548) /^.*?$/ will not match anything
- [114583](http://bugzilla.mozilla.org/show_bug.cgi?id=114583) script compile/decompile bug
- [114969](http://bugzilla.mozilla.org/show_bug.cgi?id=114969) [], [^] are valid RegExp conditions
- [115717](http://bugzilla.mozilla.org/show_bug.cgi?id=115717) java.lang.ArrayIndexOutOfBoundsException on with/try/finally
- [120194](http://bugzilla.mozilla.org/show_bug.cgi?id=120194) JS toInt32(x) conversion doesn't match ECMAScript definition
- [122167](http://bugzilla.mozilla.org/show_bug.cgi?id=122167) string.replace() placeholder '$1' not working
- [123439](http://bugzilla.mozilla.org/show_bug.cgi?id=123439) Backreferences /(a)? etc./ must hold `undefined` if not used
- [124508](http://bugzilla.mozilla.org/show_bug.cgi?id=124508) regexp.lastIndex should be integer-valued double, not uint32
- [124900](http://bugzilla.mozilla.org/show_bug.cgi?id=124900) arguments object storing duplicate parameter values
- [125562](http://bugzilla.mozilla.org/show_bug.cgi?id=125562) Regexp performance improvement
- [126317](http://bugzilla.mozilla.org/show_bug.cgi?id=126317) Crash on re.exec(str) if re.lastIndex set to certain values
- [126722](http://bugzilla.mozilla.org/show_bug.cgi?id=126722) (undefined === null) evaluating to true in Rhino compiled mode
- [128468](http://bugzilla.mozilla.org/show_bug.cgi?id=128468) java.io.NotSerializableException: org.mozilla.javascript.NativeError
- [129365](http://bugzilla.mozilla.org/show_bug.cgi?id=129365) Incorrect licensing in dtoa.java
- [132217](http://bugzilla.mozilla.org/show_bug.cgi?id=132217) delete on global function should not delete the function
- [136893](http://bugzilla.mozilla.org/show_bug.cgi?id=136893) Rhino treatment of `for(i in undefined)`, `for(i in null)`
- [137181](http://bugzilla.mozilla.org/show_bug.cgi?id=137181) delete on an arguments[i] not working correctly
- [145791](http://bugzilla.mozilla.org/show_bug.cgi?id=145791) ECMA conformance: Function.prototype.apply(), Function.prototype.call()
- [149285](http://bugzilla.mozilla.org/show_bug.cgi?id=149285) Complier does not report the correct line number on SyntaxError:Invalid assignment left-hand side.
- [151337](http://bugzilla.mozilla.org/show_bug.cgi?id=151337) EcmaError.getLineSource() returns 0x0 characters.
- [153223](http://bugzilla.mozilla.org/show_bug.cgi?id=153223) New RegExp engine in Rhino
- [154693](http://bugzilla.mozilla.org/show_bug.cgi?id=154693) Interpreted mode doesn't grok different functions on different objects
- [156510](http://bugzilla.mozilla.org/show_bug.cgi?id=156510) for (i in undefined) {} should not throw TypeError
- [157196](http://bugzilla.mozilla.org/show_bug.cgi?id=157196) ScriptableObject needs custom serialization implementation
- [157509](http://bugzilla.mozilla.org/show_bug.cgi?id=157509) No error on invalid usage of \ in identifiers
- [158159](http://bugzilla.mozilla.org/show_bug.cgi?id=158159) Should Rhino support octal escape sequences in regexps?
- [159334](http://bugzilla.mozilla.org/show_bug.cgi?id=159334) The javascript functions size is limited by a bug
- [164947](http://bugzilla.mozilla.org/show_bug.cgi?id=164947) Debugging unique.js produce a stack trace and erratic results
- [166530](http://bugzilla.mozilla.org/show_bug.cgi?id=166530) ClassCostException in FunctionObject static initializer
- [169830](http://bugzilla.mozilla.org/show_bug.cgi?id=169830) Array.concat(function) doesn't add function to the array
- [173180](http://bugzilla.mozilla.org/show_bug.cgi?id=173180) Rhino UTF-8 decoder accepts overlong sequences
- [173906](http://bugzilla.mozilla.org/show_bug.cgi?id=173906) Dynamic scope not working correctly with optimzation level >= 1
- [175383](http://bugzilla.mozilla.org/show_bug.cgi?id=175383) ArrayIndexOutOfBoundsException in string.replace()
- [177314](http://bugzilla.mozilla.org/show_bug.cgi?id=177314) Rhino should allow '\400' to mean ' 0'
- [179068](http://bugzilla.mozilla.org/show_bug.cgi?id=179068) String literals in Rhino are limited to 64K
- [179366](http://bugzilla.mozilla.org/show_bug.cgi?id=179366) --> after whitespace after line start should mean comments to line end
- [181654](http://bugzilla.mozilla.org/show_bug.cgi?id=181654) Calling toString for an object derived from the Error class throws TypeError
- [181834](http://bugzilla.mozilla.org/show_bug.cgi?id=181834) wrong scope used for inner functions when compiling functions with dynamic scopes (interpreted only)
- [181909](http://bugzilla.mozilla.org/show_bug.cgi?id=181909) some regression tests for Error invalid
- [182028](http://bugzilla.mozilla.org/show_bug.cgi?id=182028) Calling has() in get() of a ScriptableObject causes getter function to not be called
- [184107](http://bugzilla.mozilla.org/show_bug.cgi?id=184107) with(...) { function f ...} should set f in the global scope
- [184111](http://bugzilla.mozilla.org/show_bug.cgi?id=184111) ArrayOutOfBounds Exception thrown when using Rhino Javascript Debugger
- [185165](http://bugzilla.mozilla.org/show_bug.cgi?id=185165) Decompilation of "\\" gives broken "\"
- [189183](http://bugzilla.mozilla.org/show_bug.cgi?id=189183) Debugger source frame window layering fix
- [189898](http://bugzilla.mozilla.org/show_bug.cgi?id=189898) Broken String.replace: "XaXY".replace("XY", "--") gives --aXY