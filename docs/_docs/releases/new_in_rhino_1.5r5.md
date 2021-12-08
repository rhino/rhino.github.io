---
title: New in Rhino 1.5R5
parent: Releases
nav_order: -6
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
This is a log of significant changes in Rhino 1.5 Release 5.

## Wrapping of JavaScript functions as Java interfaces
Rhino allows to pass a JavaScript function to a Java method expecting an interface which either has a single method or all its methods have the same number of parameters and each corresponding parameter has the same type. The JavaScript function will be called whenever interface's method is called from Java. The function will receive all Java arguments properly converted into JS types and as the last parameter Rhino will pass interface method's name.

The feature allows to simplify code that previously had to create explicit JavaAdapter objects. For example, one can write now:

```js
    var button = new javax.swing.JButton("My Button");
    button.addActionListener(function(e) {
        java.lang.System.out.println("Button click:"+e);
    }); 
    var frame = new javax.swing.JFrame("My Frame");
    frame.addWindowListener(function(e, methodName) {
        java.lang.System.out.println("Window event:"+e);
        if (methodName == "windowClosing") {     
            java.lang.System.exit(0);
        }
    });
``` 
instead of
```js
    var button = new javax.swing.JButton("My Button");
    button.addActionListener(new java.awt.event.WindowListener({
        windowClosing : function(e) {
            java.lang.System.out.println("Window event:"+e);
            java.lang.System.exit(0);
        },
        windowActivated : function(e) {
            java.lang.System.out.println("Window event:"+e);
        },
        // similar code for the rest of WindowListener methods
    });
    var frame = new javax.swing.JFrame("My Frame");
    frame.addWindowListener(function(e, methodName) {
```
which was necessary in the previous version of Rhino. See Bugzilla 223435](https://bugzilla.mozilla.org/show_bug.cgi?id=).

## uneval() and toSource()
Rhino fully supports `uneval() `function and `toSource()` method which are extensions to ECMAScript available in SpiderMonkey. They return a string that can be passed to the `eval()` function to reconstruct the original value when possible. It is guaranteed that `uneval(eval(uneval(x))) == uneval(x)` and in many cases more useful notion `eval(uneval(x)) == deep_copy_of_x` holds.

For example, here is an extract from a [Rhino shell](../../_tools/shell.md) session:

```sh
js> var x = { a: 1, b: 2, c: [1,2,3,4,5], f: function test() { return 1; }, o: { property1: "Test", proeprty2: new Date()}}
js> uneval(x)
({c:[1, 2, 3, 4, 5], o:{property1:"Test", proeprty2:(new Date(1076585338601))}, f:(function test() {return 1;}), a:1, b:2})
js> x.toSource()
({c:[1, 2, 3, 4, 5], o:{property1:"Test", proeprty2:(new Date(1076585338601))}, f:(function test() {return 1;}), a:1, b:2})
js> uneval(x.propertyThatDoesNotExist)
undefined
```
See [Bugzilla 225465](https://bugzilla.mozilla.org/show_bug.cgi?id=225465).

## seal() and changes in semantic of sealed objects
Rhino supports `seal(object)` function which is another ECMAScript extension from [SpiderMonkey](https://spidermonkey.dev/). The function makes the object immune to changes and any attempt to add, modify or delete a property of such object will throw an exception. Previously sealing was only possible through the Java `sealObject()` method in [org.mozilla.javascript.ScriptableObject](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/ScriptableObject.html) and before Rhino 1.5R5 it was possible to modify existing properties of sealed objects.

See [Bugzilla 203013](https://bugzilla.mozilla.org/show_bug.cgi?id=203013).

## Exception changes
In Rhino 1.5R5 all exceptions generated during execution of a script provide information about script's source name and line number that triggered the exception. The exception class [org.mozilla.javascript.JavaScriptException](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/JavaScriptException.html) is used now only to represent exceptions explicitly thrown by the JavaScript **throw** statement, it never wraps exceptions thrown in a Java method invoked by the script. Such exceptions are always wrapped as (org.mozilla.javascript.WrappedException)[https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/WrappedException.html].

See [Bugzilla 217584](https://bugzilla.mozilla.org/show_bug.cgi?id=217584), [Bugzilla 219055](https://bugzilla.mozilla.org/show_bug.cgi?id=219055) and [Bugzilla 225817](https://bugzilla.mozilla.org/show_bug.cgi?id=225817)

## Compiled scripts are scope independent
Previously Rhino required a scope object in the [compileReader](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#compileReader-org.mozilla.javascript.Scriptable-java.io.Reader-java.lang.String-int-java.lang.Object-) method of [org.mozilla.javascript.Context](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html) to compile a script into [org.mozilla.javascript.Script](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Script.html) instances. Under some circumstances it was possible that the scope object would be stored in the compiled form of the script. It made impossible in such cases to reuse of the compiled form to execute the script against different scopes and lead to potential memory leaks.

Rhino 1.5R5 fixes such misbehavior and [compileReader](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#compileReader-java.io.Reader-java.lang.String-int-java.lang.Object-) and newly introduced [compileString](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#compileString-java.lang.String-java.lang.String-int-java.lang.Object-) no longer take the scope argument. For compatibility the old form of [compileReader](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#compileReader-org.mozilla.javascript.Scriptable-java.io.Reader-java.lang.String-int-java.lang.Object-) is kept as a deprecated method.
See [Bugzilla 218440](https://bugzilla.mozilla.org/show_bug.cgi?id=218440).

## Callable interface
All [org.mozilla.javascript.Script](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Script.html) and [org.mozilla.javascript.Function](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Function.html) instances in Rhino now implement the new interface [org.mozilla.javascript.Callable](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Callable.html) which together with the new [call](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Callable.html#call-org.mozilla.javascript.Context-org.mozilla.javascript.Scriptable-org.mozilla.javascript.Scriptable-java.lang.Object:A-) method in [org.mozilla.javascript.Context](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html) gives a simple way to call scripts and functions without explicit calls to [Context.enter()](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#enter--) and [Context.exit()](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#exit--).

The [Callable](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Callable.html) interface allows to set the value of JavaScript **this** during script execution to arbitrary [org.mozilla.javascript.Scriptable](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Scriptable.html) instance overriding default behaviour of using the scope object for the value of **this**.

Rhino interpreter uses [Callable](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Callable.html) to pass references to scripts and functions to [org.mozilla.javascript.SecurityController](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/SecurityController.html) directly without wrapping script code into an additional proxy [Script](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Script.html) object. It allows to optimize an implementation of [callWithDomain](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/SecurityController.html#callWithDomain-java.lang.Object-org.mozilla.javascript.Context-org.mozilla.javascript.Callable-org.mozilla.javascript.Scriptable-org.mozilla.javascript.Scriptable-java.lang.Object:A-) method in [org.mozilla.javascript.SecurityController](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/SecurityController.html).

For compatibility applications extending the previous version of [SecurityController](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/SecurityController.html) are fully supported but the new applications should override [callWithDomain](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/SecurityController.html#callWithDomain-java.lang.Object-org.mozilla.javascript.Context-org.mozilla.javascript.Callable-org.mozilla.javascript.Scriptable-org.mozilla.javascript.Scriptable-java.lang.Object:A-) method, not [execWithDomain](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/SecurityController.html#execWithDomain-org.mozilla.javascript.Context-org.mozilla.javascript.Scriptable-org.mozilla.javascript.Script-java.lang.Object-).

## No static caching
Rhino no longer caches generated classes and information about reflected Java classes in static objects. Instead such caches are stored in a top scope object and initialized by default during call to [initStandardObjects](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#initStandardObjects--) of [org.mozilla.javascript.Context](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html). This can be overridden with the explicit call to the [associate](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/ClassCache.html#associate-org.mozilla.javascript.ScriptableObject-) method of [org.mozilla.javascript.ClassCache](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/ClassCache.html) if cache sharing is desired.

The cached objects no longer holds references to scope objects so even an application using multiple calls to [Context.initStandardObjects](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#initStandardObjects--) and single shared [ClassCache](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/ClassCache.html) instance would not leak references to runtime library instantiations as it was the case with the previous Rhino for all applications.

The change allows to instantiate multiple Rhino runtime instances which would not interfere with each other and prevents memory leaks through ever growing caches.

## API for compiling scripts into class files
The new class [org.mozilla.javascript.optimizer.ClassCompiler](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/optimizer/ClassCompiler.html) provides a simple API to compile JavaScript source into set of Java class files with the given set of compilation options. [JavaScript Compiler](../../_tools/javascript_compiler.md) was upgraded to use new API and the old API were deprecated.

## API for Context sealing
The new methods [seal(Object)](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#seal-java.lang.Object-), [unseal(Object)](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#unseal-java.lang.Object-) and [isSealed()](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html#isSealed-) in [org.mozilla.javascript.Context](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html) allows to make [Context](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/Context.html) instances immune from changes. Rhino embeddings that needs to run potentially untrusted scripts may use the new functionality to proprly implement the sandbox for such scripts without too restrictive [org.mozilla.javascript.ClassShutter](https://mozilla.github.io/rhino/javadoc/org/mozilla/javascript/ClassShutter.html) implementation.

See [Bugzilla 236117](https://bugzilla.mozilla.org/show_bug.cgi?id=236117).

## Optimizer generates only one class per script
In Rhino 1.5R5 the default optimization mode generates only one Java class for script and all its functions while previously the optimizer generated additional class for each function definition in the script. It improves loading time for scripts and decreases memory usage especially for scripts with many function definitions.

See [Bugzilla 198086](https://bugzilla.mozilla.org/show_bug.cgi?id=198086).

## Improved support for huge scripts
The interpreted mode contains significantly less restrictions on size and complexity of the scripts and if the remaining restrictions are not satisfied, Rhino will report an exception instead of generating corrupted internal byte code for interpreting.

See [Bugzilla 225831](https://bugzilla.mozilla.org/show_bug.cgi?id=225831).

## Resolved Bugzilla reports
The full list of Bugzilla reports addressed in Rhino 1.5R5 can be obtained with the following Bugzilla [query](http://bugzilla.mozilla.org/buglist.cgi?product=Rhino%20graveyard&target_milestone=1.5R5&bug_status=RESOLVED&bug_status=VERIFIED) which searches bugzilla.mozilla.org for all resolved or verified bugs with the product set to Rhino and the target milestone set to 1.5R5.