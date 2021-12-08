---
title: New in Rhino 1.7.8
parent: Releases
nav_order: -21
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Most important changes in this release:

- JavaScript objects are no longer (somewhat) thread-safe by default
- Rhino is resistant to "hash flooding" attacks
- Rhino is only supported for Java 8 and up
- Rhino only builds with Gradle.

The primary change in this release is that the object storage format has changed
for objects derived from ScriptableObject (which is nearly all objects).

First, objects are no longer thread-safe by default. (They were thread-safe previously, but
not in a way that we could prove was 100 percent correct in all cases.) We do not believe
that the vast majority of Rhino code depended on this capability. 

The feature flag Context.FEATURE_THREAD_SAFE_OBJECTS may be used to enable locking on all
objects by default in case it is needed. Furthermore, the built-in "sync" function is still
supported, which can be used to wrap a function in a similar way to the "synchronized" keyword
in Java.

Second, when an object grows to a large number of properties, the native hash table implementation
is replaced with java.util.HashMap. This more complex (but slightly slower) hash implementation
is resistant to hash collisions. This makes Rhino in general resistant to "hash flooding" attacks.

Rhino now depends on Java 8. It also works on Java 9, although a few tests are currently breaking
around Date parsing and UTF-8 encoding.

Additional changes:

[Issue 290](https://github.com/mozilla/rhino/issues/290) Resist hash flooding attacks
[Issue 303](https://github.com/mozilla/rhino/issues/303) Arrow function position set error
[Issue 323](https://github.com/mozilla/rhino/issues/323) Possible OutOfMemory due to infinite loop on parsing
[Issue 341](https://github.com/mozilla/rhino/issues/341) Objects are only thread-safe when feature is enabled
[Issue 351](https://github.com/mozilla/rhino/issues/351) Function-level use-strict breaks backward compatibility
[Issue 357](https://github.com/mozilla/rhino/issues/357) Array.sort() can throw ArrayIndexOutOfBoundsException
[Issue 295](https://github.com/mozilla/rhino/issues/295) Change WrapFactory to only wrap "true" primitive types and not subclasses.
[Issue 377](https://github.com/mozilla/rhino/issues/377) Context initialization in  "sealed" mode failed for ES6 language level.
[PR102](https://github.com/mozilla/rhino/pull/102) Fix regexp parsing for "/0{0/"
[PR108](https://github.com/mozilla/rhino/pull/108) Attach jsdoc nodes to function params.
[PR 169](https://github.com/mozilla/rhino/pull/169) Enable calling default method on Java 8.
[PR322](https://github.com/mozilla/rhino/pull/322) Fix static array functions
[PR353](https://github.com/mozilla/rhino/pull/353) Member box call error.
[PR355](https://github.com/mozilla/rhino/pull/358) Support array-like parameters to  Function.prototype.apply().
[PR372](https://github.com/mozilla/rhino/pull/372) Improve test262 integration and enable many more tests.