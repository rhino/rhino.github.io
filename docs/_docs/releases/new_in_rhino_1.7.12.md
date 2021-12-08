---
title: New in Rhino 1.7.12
parent: Releases
nav_order: -25
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## XML external entities disabled by default

As of this release, Rhino makes "XML external entity injections" more difficult by disabling fetching of external DTDs and stylesheets by default, as recommended in the (OWASP Cheat Sheet)[https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.md]. Even though this may break some existing projects, the fact that this vulnerability is in the OWASP top 10 makes it important enough to change the default.

Developers who still need this old capability can re-enable it by setting the Context feature flag FEATURE_ENABLE_XML_SECURE_PARSING to false. (The default is true.)

## New JAR for embedding use cases

This release also includes a second JAR artifact, "rhino-runtime.jar". This is simply the existing Rhino JAR with the "tools" source directory excluded. This directory includes the Rhino shell as well as the default "Global" object, which includes capabilities to load and process external source code.

Since some automated source-scanning tools mark these capabilties as insecure, this new JAR provides a way to only include the parts of Rhino that embedders typically need without pulling in additional capabilities.

Developers who typically embed "rhino.jar" might consider embedding "rhino-runtime.jar" instead if they do not need all this.

Thanks to the following developers for the contributions below!

Aditya Pal (1):
- Fix syntax error for comments in array (#607)

Chris Smith (1):
- Adding secure configuration for XML parsers (#600)

Gregory Brail (12):
- Update versions for 1.7.12 release.
- Fix a code generation bug for generators.
- Fix "fall through" comment.
- Fix static analysis around NaN values.
- More isNaN fixes and one rounding bug.
- Make XML processor configuration more robust.
- Enable SpotBugs plugin.
- Fix minor static analysis findings.
- Increase Travis timeout.
- Disable more flaky "BigO" tests.
- Fix handling of "return" in iterators.
- Undo setting some members "final".

Ivan Di Francesco (1):
- Fix warnings (#596)

Roland Praml (2):
- FIX: NativeJavaObject.getDefaultValue recognizes numbers correctly
- #511 fixing InterfaceAdapter abstract name lookup.

Stijn Kliemesch (7):
- Private static method ScriptRuntime.enumInitOrder(Context,IdEnumeration) no longer expects given IdEnumeration's property obj to be of type ScriptableObject specifically, only of type SymbolScriptable.
- Added testclass IterableTest to test iterable implementations, currently with one testcase for a host object, specifically one that uses Array Iterator.
- Added more tests to IterableTest.
- Fix for #616 (#617)
- Fixes for calling several Object.prototype members.
- Fixed dynamic scoping for implementations of Object.create and Object.defineProperties
- Testcase for dynamic scoping and Object.create.

nename0 (2):
- Fix Array.include return a wrapped Boolean
- implement Array.includes to align to specs

RBRi (20):
- fix for Map/Set working with ConsString as key also; closes #583
- fix propertyIsEnumerable when using an index to access string; closes #582
- ignore surplus search/match/replace parameters; closes #581
- add support for setPrototypeOf
- fixed imports
- RangeError should be throw if the argument of Number.prototype.toFixed is less than 0 fixes #587
- fix interpreter fallback when using streams (fixes #592)
- Parser already always reads the reader into a string. Move this reader handling to the Context to be able to fall back to the interpreter in all cases.
- fix imports
- functions declared as var f = function f() {...} within a function should not impact higher scope variable with the same name
- functions declared as var f = function f() {...} within a function should not impact higher scope variable with the same name
- fix Boolean(document.all)
- many more tests are passing already and some cleanup
- add tests for built-ins/ThrowTypeError and built-ins/TypedArray
- add tests for built-ins/TypedArrays
- fix BYTES_PER_ELEMENT property
- fix BYTES_PER_ELEMENT prototype property
- fix TypedArray constructor arity
- Fix issue with parseInt's handling of leading zeroes
- #529 (#628)