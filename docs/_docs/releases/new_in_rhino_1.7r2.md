---
title: "New in Rhino 1.7R2"
parent: Releases
---
# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## Java API for Continuations

Rhino has supported Continuations for some time now, but there wasn't a great way to interact with continuations from Java. Continuations have been useful with in server-side scripting, since it allows for saving and restarting JavaScript execution, possibly with serializing the execution state when stopped. With Rhino 1.7R2, methods in `org.mozilla.javascript.Context` allow for control from Java:

- [executeScriptWithContinuations](javadocs/org/mozilla/javascript/context.html#executescriptwithcontinuations(org.mozilla.javascript.script,%20org.mozilla.javascript.scriptable)) - Execute script that may pause execution by capturing a continuation.
- `callFunctionWithContinuations - Call function that may pause execution by capturing a continuation.`
- [captureContinuation](javadocs/org/mozilla/javascript/context.html#capturecontinuation()) - Capture a continuation from the current execution.
- [resumeContinuation](javadocs/org/mozilla/javascript/context.html#resumecontinuation(java.lang.object,%20org.mozilla.javascript.scriptable,%20java.lang.object)) - Restarts execution of the JavaScript suspended at the call to captureContinuation.

For example, if you had a Java class MyClass with a method f(). Say that you wanted to pause execution of a script when f() was called. You could call captureContinuation, which wraps up all the state of the current execution and returns it as a ContinuationPending object. ContinuationPending is also an exception; you indicate to Rhino that you want to suspend execution by throwing the exception:

```
public static class MyClass {
    public int f(int a) {
        Context cx = Context.enter();
        try {
            ContinuationPending pending = cx.captureContinuation();
            pending.setApplicationState(a);
            throw pending;
        } finally {
            Context.exit();
        }
    }
}
```

Rhino only allows capturing continuations in scripts that are exeucting when called in through new Context methods, executeScriptWithContinuations and callFunctionWithContinuations. If a Java method called while executing using these methods throws ContinuationPending, the exception is propagated up, allowing the calling Java code to perform some action and then resume execution later:

```
Context cx = Context.enter();
try {
    cx.setOptimizationLevel(-1); // must use interpreter mode
    Script script = cx.compileString("myObject.f(3) + 1;",
        "test source", 1, null);
    cx.executeScriptWithContinuations(script, globalScope);
    fail("Should throw ContinuationPending");
} catch (ContinuationPending pending) {
    Object applicationState = pending.getApplicationState();
    assertEquals(new Integer(3), applicationState);
    int saved = (Integer) applicationState;
    Object result = cx.resumeContinuation(pending.getContinuation(),
        globalScope, saved + 1);
    assertEquals(5, ((Number)result).intValue());
} finally {
    Context.exit();
}
```
Note also that as an added convenience ContinuationPending supports saving an application-defined object. The continuations API is only supported for interpreted mode.

For more examples of using the API, see the unit test, [ContinuationsAPITest.java](https://github.com/mozilla/rhino/testsrc/org/mozilla/javascript/tests/ContinuationsApiTest.java).

## Better line editing for Rhino shell

Rhino 1.7R2 now has line editing in the Rhino shell. The heavy lifting comes from [JLine](https://jline.sourceforge.net/), a nice Java library for handling console input. We get command history (using the up and down arrow keys to bring up previous command lines) for free. And with some additional code in Rhino we have limited support for completion.

We don't ship with JLine with Rhino, so you'll have to download it yourself. Rhino automatically detects whether JLine is on the classpath and uses it if so and otherwise maintains the previous simple behavior. So to run your shell with JLine your command will look like

```
java -cp js.jar:lib/jline-0.9.93.jar org.mozilla.javascript.tools.shell.Main
```

Completion works by looking at the global scope and attempting to complete variables defined there. For example,

```
js> var obj = {prop1:{prop2:3}};
js> ob
```

After typing `ob` and pressing tab, Rhino will autocomplete to `obj`. It's also smart enough if it sees a dotted property list it will walk it to find names to autocomplete:

```
js> obj.prop1.pr
```

Pressing tab after `obj.prop1.pr` will autocomplete to `obj.prop1.prop2`.

Autocompletion also works for Java objects:

```
js> var s = new java.lang.String("hi");
js> s.
```

Pression tab after "s." will cause Rhino to list all the possible completions:

```
contentEquals(         bytes                  codePointBefore(
hashCode(              contains(              indexOf(
wait(                  isEmpty(               toUpperCase(
matches(               substring(             notify(
empty                  equalsIgnoreCase(      length(
getChars(              replaceFirst(          codePointAt(
codePointCount(        trim(                  charAt(
notifyAll(             subSequence(           getClass(
getBytes(              startsWith(            equals(
class                  lastIndexOf(           compareTo(
offsetByCodePoints(    concat(                replace(
compareToIgnoreCase(   toCharArray(           toLowerCase(
intern(                chars                  split(
toString(              replaceAll(            endsWith(
regionMatches(
```

Some limitations: it's not possible as far as I know to enumerate all the classes or packages in the Java runtime, so autocompletion works somewhat disappointingly for Java class names. I've also found that JLine doesn't work in the Eclipse console, so I just leave the JLine jar off when I'm running in Eclipse.

For more details, see [bug 418034](https://bugzilla.mozilla.org/show_bug.cgi?id=418034).

## Debugger bundled with Rhino distribution

Thanks to the sharp eyes of Hannes Wallnoefer, who spotted a more-liberally licensed version of files we depended on for the Rhino debugger GUI, we now have the debugger fully built and shipped with Rhino.

See [Rhino License](license.md) for details on the new license for files in the debugger.

## Doctest

Python is a fertile ground of good ideas, and we've seen a number of Python's ideas surface in JavaScript recently. JavaScript 1.7's [generators](https://web.archive.org/web/20210502042346mp_/https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.7#Generators)and [array comprehensions](https://web.archive.org/web/20210502042346mp_/https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.7#Array_comprehensions) are two recent examples.

Rhino 1.7R2 contains another Python idea: [doctest](https://docs.python.org/lib/module-doctest.html). This is a function that will test snippets of shell sessions. It gets its name from its use testing these snippets that appear in documentation comments, but it turns out to be a very convenient way to write tests more generally.

For example, say you've written a new function `hello()`. I usually go to the shell and play with it to make sure it works correctly:

```
js> function hello(greetee) {
  >   return "hello, " + greetee;
  > }
js> hello("world");
hello, world
js> hello(3)
hello, 3
js> hello()
hello, undefined
```

Now to test this function you might write a  [JUnit](https://www.junit.org/) test that executes a bunch of setup code and then calls `hello()` three times, saving the result value, and calling a comparison function with the actual and expected values. It's a decent amount of code to write.

Doctest does this all for me. Rhino 1.7R2 contains both a new doctest shell function and a JUnit test [DoctestsTest](https://github.com/mozilla/rhino/testsrc/org/mozilla/javascript/tests/DoctestsTest.java) that finds files with a `.doctest` extension and runs them. So now all I need to do is copy the shell session above, paste it into `hello.doctest`, and put it in the right directory and I have a JUnit test! It's much more convenient to write tests, which greatly increases the chances that tests actually get written.