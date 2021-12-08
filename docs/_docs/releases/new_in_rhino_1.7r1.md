---
title: New in Rhino 1.7R1
parent: Releases
nav_order: -14
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Rhino 1.7R1 is a major feature release.

## JavaScript 1.7 features

As of Rhino1.7R1, Rhino now supports the features of JavaScript 1.7. See [New in JavaScript 1.7](https://web.archive.org/web/20210502042346mp_/https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.7). JavaScript 1.7 supports the following features:

- Generators and iterators
- Array comprehensions
- Block scope with let
- Destructuring assignment

To enable JavaScript 1.7 support, you must set the version as 170 using the `Context.setLanguageVersion()` API call. If you are using the Rhino shell, you can specify `-version 170` on the command line or call `version(170)` in code executed by the shell.

## Creating a JavaScript `Iterator` from a Java `Iterable` or `Iterator`

In an extension to JavaScript 1.7, Rhino now supports creating JavaScript `Iterators` from [java.lang.Iterable](https://java.sun.com/javase/6/docs/api/java/lang/Iterable.html) and [java.util.Iterator](https://java.sun.com/javase/6/docs/api/java/util/Iterator.html) objects. For example:

```
js> m = new java.util.LinkedHashMap()
{}
js> m.put("a",1); m.put("b",2); m
{a=1.0, b=2.0}
js> for (i in Iterator(m.values())) print(i)
1.0
2.0
js> for (i in Iterator(m.values().iterator())) print(i)
1.0
2.0
```

Note that `for (i in m.values())` will still iterate over the properties of the object returned by `m.values()`, i.e., the names of all the methods of `java.util.HashMap$Values`. This was done so as not to compromise backwards compatibility.

## DOM3 E4X implementation preferred

As of Rhino 1.7R1, the E4X implementation based on DOM3 is now preferred over the XMLBeans implementation. Previously the XMLBeans implementation would be used if present in the classpath; now it will be used only if DOM3 is not supported on the version of Java running Rhino (i.e., before JDK 1.5), or if explicitly specified by overriding `ContextFactory.getE4xImplementationFactory()`.

## Support for JDK 1.4 through separate JAR file

We now require at least JDK 1.5 in order to compile Rhino sources. As a result, the `js.jar` in the binary distribution is not runnable with JDK 1.4. In order to support people running Rhino on JDK 1.4, we use [Retrotranslator](https://retrotranslator.sourceforge.net) to produce `js-14.jar`, which is compatible with JDK 1.4. `js-14.jar` is also in the binary distribution and can be built from source using ant.
JDK 1.4 support will be dropped entirely from Rhino in a future release.

## Support for instruction threshold callbacks in compiled mode

It's now possible to request instruction callbacks for compiled scripts. This is primarily used to enforce instruction quotas for untrusted scripts. See [bug 397680](https://bugzilla.mozilla.org/show_bug.cgi?id=397680).

## `debugger` keyword

Fix [bug 386997](https://bugzilla.mozilla.org/show_bug.cgi?id=386997) - Need to support 'debugger' statement
Adding the 'debugger' keyword will now result in a breakpoint being hit when
run in the Rhino debugger. The statement is ignored if the debugger is not
running or when compiled to Java bytecodes.

## Common package names preloaded

Prior to 1.7R1, Java classes in packages starting with "java." could be referenced directly, while classes in other packages would need to use the "Packages" object first. Now the following top-level packages are available, like "java", in the global scope: "javax", "org", "com", "edu", and "net".

## Array and String generics

See [New in JavaScript 1.6](https://web.archive.org/web/20210502042346mp_/https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.6). This feature is now implemented in Rhino.

## Configurable prompts in the shell

If a global variable `prompts` is defined, is an object, and has elements 0 and 1 defined, the shell will use element 0 as the prompt and element 1 as the continuation prompt. If the array elements are functions, Rhino will call them:

```
js> function f() {
  >   return 3;
  > }
js> f();
3
js> var prompts = true;
js> var prompts = true; // won't affect shell prompts
js> var prompts = [">>> ", "... "];
>>> function g() {
...   return 3;
... }
>>> g()
3
>>> var prompts = {count:0, 0:function(){ return this.count++ + "> "; }, 1:">> "};
0> function h() {
>>   return 5;
>> }
1> h();
5
2>
```

## Debugger must be built after download

Well, this isn't a feature, but to ensure we're not shipping binaries built from sources that are not available under an open source license, you must download some source files and build the debugger yourself. Here's how to do it:

- `unzip rhino1_7R1.zip`
- `cd rhino1_7R1`
- `ant compile-debugger`

Now `js.jar` contains the sources needed to run the debugger:

```
java -cp js.jar org.mozilla.javascript.tools.debugger.Main test.js
```

And if anyone would like to contribute changes that allow us to build the debugger without depending on these closed-source licenses, we'd be happy to take those changes into Rhino.

---

Norrisboyd 07:03, 13 June 2007 (PDT)