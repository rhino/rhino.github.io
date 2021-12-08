---
title: New in Rhino 1.7.13
parent: Releases
nav_order: -26
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## Script Engine support

Now that Nashorn has been deprecated, a number of people have asked about using Rhino with the standard Java "ScriptEngine" interface. This release supports that.

However, in order to avoid breaking existing code, the script engine is shipped in a separate JAR. Use the "rhino-engine" jar along with the standard "rhino" jar to include this feature.

## Generator Support

This release supports generators based on the ES6-standard `function *` syntax.

## Other important changes

This release also includes a number of quality and consistency fixes from five contributors. As always, check out the [compatibility table](https://mozilla.github.io/rhino/compat/engines.html) to see where Rhino stands today.

Gregory Brail (18):
- Start on 1.7.13.
- Add a build config for CircleCi.
- Upgrade Gradle version to 6.5.
- Update max workers.
- Add support for ES6 generators.
- Make "GeneratorFunction" pattern work in interpreted mode.
- Complete implementation of GeneratorFunction.
- Diagnostics to discover test timeouts.
- Implement standard Java ScriptEngine
- Change MozillaSuiteBenchmark to not fork threads.
- Try to improve performance of MozillaSuiteTest
- Disable some very slow tests
- Start using JMH for benchmarks.
- Many small fixes suggested by FindBugs and other linters
- Turn off all the Mozilla tests that use the "BigO" function.
- Move "BodyCodegen" into a file with the appropriate name.
- Add feature flag for changes to Function.\_\_proto\_\_
- Make \_\_proto\_\_ more closely match the spec

Karl Tauber (2):
- Debugger fixes for [FlatLaf](https://github.com/JFormDesigner/FlatLaf):
  - make renderer tree row height same as table row height
  - increase monospaced font size in script source and evaluation view if L&F uses larger font
  - remove renderer tree border if L&F sets one (built in L&F do not)
- Debugger: fix NPE in variables view when expanding "CallSite"

Sylvain Jermini (7):
- improve java.util.{List,Map} interop
- travis: switch from trusty to xenial + set explicit -Xss in tests
- try to fix circle, increase Xss
- Fix failing string.trim.doctest in java11.
- NativeDate: DateFormat, use explicit pattern, has the default has changed from java8 to 9. See https://stackoverflow.com/q/53317365
- add java11 to travis test matrix
- various fixes so the javadoc linter is happy

hjx胡继续 (2):
- Add String.fromCodePoint()
- fromCharCode optimize

ian4hu (5):
- Add String.prototype.trimStart String.prototype.strimEnd
- style: code style
- test: string test with hex code instead of literal
- remove unused StringBuilder
- fix tests in test262/built-ins/String/fromCodePoint/*

leela52452 (1):
- fix OWASP Cheat Sheet markdown format

RBRi (48):
- switch value and done
- make some method protected to support rhino-external implementations
- NativeArrayBuffer slice() length is 2
- fix String.indexOf and String.includes when searching for an empty st… [#747](https://github.com/mozilla/rhino/issues/747)
- fix string.split with limit 0
- fix for issue [#665](https://github.com/mozilla/rhino/issues/665) (maybe we have to adjust the version switch to version 1_6)
- fix for the recursion detection when converting an array into a string
- fix [#670](https://github.com/mozilla/rhino/issues/670)
- add testcase for issue [#656](https://github.com/mozilla/rhino/issues/656)
- Symbol.length is 0 fixes [#648](https://github.com/mozilla/rhino/issues/648)
- add testcase for issue [#651](https://github.com/mozilla/rhino/issues/651)
- fix type o the expected value
- improve seal() and freeze() processing; fixes [#174](https://github.com/mozilla/rhino/issues/174)
- An error should be thrown when defining a property for a read-only variable in strict mode fixes 573
- code cleanup
- Do not save/share an instance of NativeArrayBuffer in a static variable. This introduces really strange side effects, because the instance is available (and changeable) from javascript code. These changes are 'persistent' in a way that starting a fresh rhino instance still uses this changed object.
- various fixes for array calls using this pattern Array.prototype.foo.call(null, ....);
- fix issue [#648](https://github.com/mozilla/rhino/issues/648)
- fix Object.getOwnPropertyDescriptor for index properties on native strings
- Function.\_\_proto\_\_ ignores write access
- improved regexp parser based on commit 2164382abe078ea2024b9dff7fe416a78e3a668f from anba
- fix handling of undefined parameter value in String.normalize()
- it should not be possible to change the [[Prototype]]  of a non-extensible object; some cleanup
- add version guard
- fix all this-value-not-obj-coercible.js tests for string
- checkstyle fixes
- fix test suite setup
- use the RangeError construction helper
- improved handling of negative ArrayBuffer size fixes [#708](https://github.com/mozilla/rhino/issues/708)
- in ES6 TypedArray constructors are only callable via new
- avoid some auto boxing use Double.valueOf instead of new some cleanup try to optimize the code a bit to avoid unnecessary conversations and Double object creation make some methods static
- regular expressions are not functions in the context of string replace fixes [#726](https://github.com/mozilla/rhino/issues/726)
- improved regex range handling
- do not inherit strict mode when parsing a function body
- code style fix
- fix wrong start object for getter in Object.assign
- use Undefined.isUndefined()
- String.prototype[Symbol.iterator].call(undefined) has to throw because undefined is not coercible
- enable more test cases
- reduce auto boxing to be able to better control this and avoid boxing if possible
- make a bunch  of methods static
- code cleanup
- make the inner class static (this makes also SpotBugs happy)
- Object.setPrototypeOf() arg[0] has to be coercible
- fix one more case
- match
- search
- throw if the lastIndex prop of an regex is readonly