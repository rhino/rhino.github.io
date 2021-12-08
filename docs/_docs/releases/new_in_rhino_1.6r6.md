---
title: New in Rhino 1.6R6
parent: Releases
nav_order: -12
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Rhino 1.6R6 adds several new features.

## JavaScript 1.5 features

Rhino now supports the remaining JavaScript 1.5 features that hadn't been implemented in previous Rhino versions.

### JavaScript 1.5: "strict" mode with new warning messages

See [Tackling JavaScript strict warnings](https://www.javascriptkit.com/javatutors/serror.shtml) for a description of JavaScript strict mode.

Briefly, Rhino reports warnings in strict mode for

- assignments to undefined variables
- references to undefined properties
- inconsistent return statements in a function
- duplicate parameter names
- variables that hide parameters
- assignment in a conditional (_Note: you can suppress this warning by including an extra set of parentheses around the assignment_)
- trailing comma in object initializer (_Note: this is always a full error in Rhino_)
- indirect calls to eval
- useless expressions

To enable strict mode for the Rhino shell, add `-strict` to the command line. If you are using the API directly, set the Context feature `FEATURE_STRICT_MODE`.

It's also possible to cause all warnings to be treated as errors. Add `-fatal-warnings` to the shell command line or set the Context feature `FEATURE_WARNING_AS_ERROR`.

See [bug 378790](https://bugzilla.mozilla.org/show_bug.cgi?id=378790) for nitty gritty details.

### JavaScript 1.5: Getters and Setters

See [Defining Getters and Setters](https://developer.mozilla.org/en-US/docs/JavaScript/Guide/Working_with_Objects#Defining_getters_and_setters) in the JavaScript 1.5 Reference.

### JavaScript 1.5: `const` keyword

See [const](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Statements/const) in the JavaScript 1.5 Reference.

## New E4X Implementation using Java 1.5 DOM

Since Rhino 1.6R1, Rhino has used the Apache XMLBeans library to support E4X. In Rhino 1.6R6 the E4X support has been rewritten to rely solely on the DOM3 APIs supported natively by Java 1.5.
Pre-1.5 users can use DOM3 using Java's endorsed standards override mechanism if they have a DOM3-capable XML parser. 
As of this release, the XMLBeans implementation remains the default if XMLBeans classes are found on the classpath; otherwise, the native DOM implementation is used if DOM3 is present.
If neither XMLBeans nor DOM3 are present, E4X is not available.

## Integration with Java security architecture

Rhino 1.6R6 adds org.mozilla.javascript.PolicySecurityController as a concrete implementation of an org.mozilla.javascript.SecurityController and the preferred way of integrating with Java security architecture.
When no security controller is in use, generated classes and scripts run in the ProtectionDomain of Rhino classes.
Wrapped access to system properties and creation of class loaders into AccessController.doPrivileged() to nicely play in secured environments.

## Test Drivers

Rhino now comes with test drivers written in Java. These drivers can be used to test Rhino if you are making any changes to the core engine. They are designed to use the tests shared with the C-based SpiderMonkey engine in mozilla/js/tests in CVS.

See [Running the Rhino tests](running_the_rhino_tests.md) for details on how to execute the tests using JsDriver.

## Support for calling Java methods and constructors with variable argument lists

Java J2SE 5 added support for variable argument lists in constructors and methods. Rhino 1.6R6 now supports calling these methods and constructors using variable argument lists. For example,

```
java.lang.System.out.format("%3.1f%s\n", 1.6, "R6");
```

prints `1.6R6`.

See [bug 382457](https://bugzilla.mozilla.org/show_bug.cgi?id=382457) for more details.

## Bug fixes

This [list](https://bugzilla.mozilla.org/buglist.cgi?query_format=advanced&short_desc_type=allwordssubstr&short_desc=&product=Rhino%20graveyard&target_milestone=1.6R6&long_desc_type=substring&long_desc=&bug_file_loc_type=allwordssubstr&bug_file_loc=&status_whiteboard_type=allwordssubstr&status_whiteboard=&keywords_type=allwords&keywords=&bug_status=RESOLVED&bug_status=VERIFIED&bug_status=CLOSED&resolution=FIXED&emailassigned_to1=1&emailtype1=exact&email1=&emailassigned_to2=1&emailreporter2=1&emailqa_contact2=1&emailtype2=exact&email2=&bugidtype=include&bug_id=&votes=&chfieldfrom=&chfieldto=Now&chfieldvalue=&cmdtype=doit) shows all the bugs (and enhancements) fixed in Rhino 1.6R6.