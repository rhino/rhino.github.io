---
title: Rhino 1.5R4.1
parent: Releases
nav_order: -5
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
1.5R4.1 is a bug fix release to address mostly regressions from 1.5R3 found in 1.5R4. The only visible API change compared with 1.5R4 is two new methods in [org.mozilla.javascript.Context](/rhino/javadoc/org/mozilla/javascript/Context.html), [getApplicationClassLoader()](/rhino/javadoc/org/mozilla/javascript/Context.html#getApplicationClassLoader-) and [setApplicationClassLoader(ClasssLoader)](/rhino/javadoc/org/mozilla/javascript/Context.html#setApplicationClassLoader-java.lang.ClassLoader-). They allow to control the class loader Rhino uses when accessing application classes.
For differences between 1.5R4 and 1.5R3, see [1.5R4 change log](new_in_rhino_1.5r4.md).

## Resolved Bugzilla reports
The following Rhino reports in Bugzilla where resolved for Rhino 1.5 Release 4.
- [96270](http://bugzilla.mozilla.org/show_bug.cgi?id=96270) Unable to create java objects from within a javascript.
- [193168](http://bugzilla.mozilla.org/show_bug.cgi?id=193168) Rhino debugger in v1.5R4 fails to update script source when a script is reloaded.
- [193555](http://bugzilla.mozilla.org/show_bug.cgi?id=193555) 1.5R4 regression: function expression has no access to its name.
- [196017](http://bugzilla.mozilla.org/show_bug.cgi?id=196017) 1.5R4 regression: script can not find classes on some versions of JDK.
- [200551](http://bugzilla.mozilla.org/show_bug.cgi?id=200551) JavaAdapter not loading a class if js.jar installed in jre/lib/ext directory.