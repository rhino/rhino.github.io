---
title: Rhino 1.7.14
parent: Releases
nav_order: -27
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## January 6, 2022

# Links
* [1.7.14 milestone](https://github.com/mozilla/rhino/milestone/14)
* [All merged PRs](https://github.com/mozilla/rhino/pulls?q=is%3Apr+merged%3A2020-09-02..2022-01-06+)

# Highlights
## Features
#### ECMAScript features
* #160 Promise support (@gbrail)
* #837 BigInt support (@tuchida)
* #243 Template Literal support (@p-bakker)
* #879 String.raw (@tonygermano)
* #977 JSON superset (@tuchida)
* #932 globalThis (@p-bakker)
* #838 Exponential operator (@tuchida)
* #853 Short-hand property names (@tuchida)
* #902 Object.values / Object.entries / Object.fromEntries (@rPraml)
* #883 Number.EPSILON (@tonygermano)

#### Non-ECMAScript features
* #153 stack property on Error Constructor (@gbrail)
* #888 support for Mozilla-styled Stack formatting (@rbri)

[All features](https://github.com/mozilla/rhino/issues?q=milestone%3A%22Release+1.7.14%22+label%3Afeature+is%3Aclosed)

## (Potential) Breaking Changes
* #820 Introduced Context.FEATURE_ENABLE_JAVA_MAP_ACCESS, defaulting to false.
  This, by default, disables direct property access on Java maps from JavaScript, which got introduced in #713 and was released with Rhino 1.7.13:
  ```
  var h = new java.util.HashMap();
  h.put('a', 123);
  h.a;  // 123.0`)
  ```
  The rationale for this change can be seen in #820 and the JavaDoc on the aforementioned feature flag.

## Bugs
[All bug fixes](https://github.com/mozilla/rhino/issues?q=milestone%3A%22Release+1.7.14%22+label%3Abug)

## Performance
[All performance enhancements](https://github.com/mozilla/rhino/issues?q=milestone%3A%22Release+1.7.14%22+label%3APerformance)

## Java Interop
* #839 JavaScript for-of loop support for Java Iterables (@tuchida)
* #860 / #857 JSON.stringify support on Java Objects (@tonygermano / @rPraml)
* #1031 delete operator and .length setting support in JavaScript on Java Lists (@rPraml)
* #901 java.util.subList() support on JavaScript Arrays in Java (@rPraml)
* #889 Automatically increase size of Java List instances on .put(...) if required (@rPraml)

[All Java Interop related cases](https://github.com/mozilla/rhino/issues?q=milestone%3A%22Release+1.7.14%22+label%3A%22Java+Interop%22)

## Embedding Rhino
* #864 Context now implements Closable (@gbrail)
* #865 Introduction of LambdaFunction and LambdaConstructor, to be used to represent Java lambda functions as native JavaScript functions and also can be used to construct an entire class out of lambdas (@gbrail)
* #911 Throw InternalError instead of wrapped JavaException if thrown Java Exception class is not visible due to class shutter (@youngj)

[All Rhino embedding related cases](https://github.com/mozilla/rhino/issues?q=milestone%3A%22Release+1.7.14%22+label%3A%22embedding+Rhino%22+)

## Test262 suite
* Running against a much newer version of Test262 suite
* Improved documentation for running the Test262 suite + more options to make running the tests easier & faster
* #930 Support added for automatically regenerating the test262.properties file based on actual passage of tests
* #930 Improved feedback about reason of test failures

## Distribution
* #873 Automatic module names

## Internals
* #878 Removed idSwitch
* #896 SlotMap and Slot refactoring
* #922 Started extracting logic related to Abstract Operations as defined by the ECMAScript specification

## Misc.
* #661 Rhino now listed in the [kangax ES6 Compatibility table](https://kangax.github.io/compat-table/es6) (must select the `Show obsolete platforms` in the upperleft corner)
* #661 Rhino now available as a compilation target in Babel through @babel/preset-env:
```
{
  "targets": {
    "rhino": "1.7.13"
  }
}
```
* Introduced Java Code Formatting through spotless
* Moved to CircleCI (instead of Travis)
* Enabled Gitlab CI, running tests on multiple Java versions'

## Thanks!

This release contains more than 350 commits from 23 contributors. Thanks to everyone who helped!