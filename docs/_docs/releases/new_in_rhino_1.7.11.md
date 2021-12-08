---
title: New in Rhino 1.7.11
parent: Releases
nav_order: -24
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
This release includes implementations of a number of missing JavaScript language features, including:
- Improvement to the accuracy and reliability of the parser and its associated AST.
- The Map, Set, WeakMap, and WeakSet classes.
- More Array functions, including from, of, fill, keys, values, entries, and copyWithin.
- Many more Math methods.
- More Object functions, including seal and freeze.
- Many other bug fixes, as shown below.

In general, Rhino's philosophy for new features and changes is to follow the ECMAScript spec, but to use the "language version" on the Context class when backward compatibility would be broken.

For example, the Array.prototype.concat function in older versions of Rhino would treat any input value as "spreadable" if it has the same constructor as Array. ECMAScript now says clearly that this should only happen if the "isConcatSpreadable" symbol is present. In this release, the old behavior is disable when the language level is at least the "ES6" level (Context.VERSION_ES6, or 200).

Developers working on new code will be happier if they set the language level to CONTEXT.VERSION_ES6, or use the "-version 200" flag to the command line tool.

A future release will change the default language version of the command line tool.

This release contains contributions from 15 developers. Thanks for all your hard work!

Attila Szegedi (7):
- Improvements to MemberBox (#438)
- Labmdify usages of ContextAction
- Make ContextAction generic.
- API for comparing continuation implementations
- Algorithm for structural equality comparison of object graphs
- Use structural equality as the equality algorithm for Interpreter.CallFrame, which serves as the NativeContinuation implementation.
- Add workarounds for #437 and #449

Dimitar Nestorov (1):
- Update README.md

Dirk Hogan (1):
- 431 update expiry of cached commonjs entity if no change on filesystem

Gregory Brail (18):
- Prepare for next iteration.
- Support replacing prototype functions of native objects.
- Fix NullPointerException in __defineGetter__
- Fix a problem with standard objects that have Symbols in their  prototypes.
- Implement the built-in Set and Map classes for ES6.
- Add WeakMap and WeakSet on top of the Map and Set work.
- Upgrade max heap for Gradle tests to 1 GB.
- Test cases and a small fix for native arrays.
- Implement @@isConcatSpreadable and make Java arrays spreadable
- Code review comments for @@isConcatSpreadable.
- Make the "Sorting" helper class a proper singleton.
- Un-do recent addition to the Scriptable interface.
- Update Gradle wrapper version.
- Fix flag tests that assume Context is available.
- Fix a parser bug with missing semicolon warnings.
- Fix a regression introduced recently to MemberBox.
- More compatibility fixes for Array.prototype.concat.
- Work on Array.of, from, and copyWithin.
- Fix a parsing regression.

Igor Kuzmanenko (2):
- fixes XmlMemberGet toSource implementation (#483)
- fixes position for ParenthesizedExpression nodes (#129)

Markus Sunela (1):
- Add manual OSGi manifest

Mozilla-GitHub-Standards (1):
- Add Mozilla Code of Conduct file

Nedelcho Delchev (1):
- Update README.md

RBRi (2):
- some fixes/enhancements for the typed array support (#436)
- Array fixes (#467)
- fix all javadoc errors and all javadoc html warnings
- method Global#version(xxx) should return the new version identifier if the version was updated
- add more info to the error message
- us the right method name if available
- two minor improvements from HtmlUnit code * window list is sorted * Command 'Go to line' added
- avoid npe if no file window is available
- improve the design for flexible subclassing
- remove duplicated check
- fix the isSymbol detection to no longer detect the prototype as symbol
- we have many more 262 tests passing already - i think we have to use as many tests as possible to check our quality
- and some more; now we are at 51093
- Use as many test262 tests as possible to check our quality
- implement missing Math functions
- disable some slow tests
- Support for `arguments` object as TypedArray constructor argument this is the same as #297 but includes a simple test.
- fix issue 437
- use the system line separator for code generation
- remove work around for 437
- fix #449 also and remove the work around from EqualObjectGraphs
- add @Override and some more cleanup
- fix ctor called with date arg
- valueOf has to be called without any args
- fix remaining utc constructor case
- minor cleanup
- fix native array constructor called with null and same for the setter
- code cleanup based on eclipse Photon suggestions
- add more delegate methods to MemberBox; name all delegate method using the name of the delegated method
- avoid star imports across the codebase
- fall back to the interpreter if the byte code generation fails
- fix serialization for NativeMap, NativeSet, NativeWeakMap, and NativeWeakSet
- scope is only undefined in strict mode; fix special null entries for maps
- more config cleanup - use files for excluding; again enable a bunch of tests already running
- another VMBridge cleanup step (JDK 1.8 is the minimum at the moment)
- another map fix
- more detailed tests hack to dump already passing tests exclude one more class of tests more tests are passing
- next try to make the travis build pass
- array.fill
- array.keys, array.entries, array.values
- fixes for DataView, including enabling more test cases.
- fix freeze/preventExtensions/seal/isFrozen/isExtensible/isSealed for ES6
- add padStart and padEnd
- make serialVersionUID private
- make the test pass on my machine (also from inside eclipse)
- fix null/undefined handling add first array includes impl
- fix some array length handling border cases
- NativeArray cleanup more error output for Test262SuiteTest
- fix for #531 - using a symbol as array index crashes with a class cast exception
- Update Jacoco version
- functions are valid keys for WeakMap/WeakSet
- use valueOf
- cleanup vm bridge; since we are at java 8 there is no need to check for iterator availability
- cleanup member; we are using the executable type instead of member
- fix unused import
- another jdk check no longer required
- fix build
- add (modified) test case from #135
- first simple version of copyWithin
- first array.of impl

Raphaël Jakse (1):
- Test function arity and length properties

Ravi Kishore (1):
- Retain of comments and their position in the actual code after parsing. (#465)

Stijn Kliemesch (1):
- Added testcase for #510

Sébastien Doeraene (2):
- Fix #448: Correctly wrap the result of Math.imul as an Int32.
- Fix the conversions in typedarrays.Conversions.

Travis Haagen (2):
- Fix bug that caused modified JavaScript files to never be reloaded
- Created UrlModuleSourceProviderTest

nabice (2):
- Fix #533 AstNode.setParent() causes a position error
- test for #533

raphj (1):
- Override getArity

stijnkliemesch (1):
- Fixes Parser.throwStatement()