---
title: Rhino 1.6R1
parent: Releases
nav_order: -7
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Release Date: 2004-11-29

Rhino 1.6R1 is the new major release of Rhino. It supports ECMAScript for XML (E4X) as specified by [ECMA 357 standard](https://www.ecma-international.org/wp-content/uploads/ECMA-357_2nd_edition_december_2005.pdf). E4X is a set of language extensions adding native XML support for JavaScript without affecting the existing code base. [E4X example](https://github.com/mozilla/rhino/blob/master/examples/E4X/e4x_example.js) demonstrates various E4X constructions and their usage in JavaScript code.

This version of Rhino should be binary compatible with the current embeddings that use only public [API](https://javadoc.io/doc/org.mozilla/rhino/latestindex.html) unless the code use the previously deprected classes as documented [below](#removal-of-deprecated-classes). Please report any incompatibility issues to Bugzilla.

## E4X implementation
The E4X code was donated to the Rhino project by [BEA](http://www.bea.com/) and developed by staff from [BEA](http://www.bea.com/) and [AgileDelta](http://www.agiledelta.com/).

It uses [XMLBeans](http://xmlbeans.apache.org/) library to implement E4X runtime. The implementation was tested against versions 1.0.2 and 1.0.3 of XMLBeans. Please make sure that `xbean.jar` is avaialble on the classpath if you use E4X in your scripts.

See [Bugzilla 242805](https://bugzilla.mozilla.org/show_bug.cgi?id=242805) for details. See also [Bugzilla 270779](https://bugzilla.mozilla.org/show_bug.cgi?id=270779) for the list of known issues with E4X implementation in Rhino 1.6R1.

## Other changes
### Common root for Rhino execeptions
Now all Rhino execption classes are derived from [org.mozilla.javascript.RhinoException](https://github.com/mozilla/rhino/blob/master/src/org/mozilla/javascript/RhinoException.java) which extends `java.lang.RuntimeException`. The class gives the uniform way to access information about the script origin of the exception and simplifies execption handling in Rhino embeddings.

See [Bugzilla 244492](https://bugzilla.mozilla.org/show_bug.cgi?id=244492) for details.

### Removal of code complexity limits in the interpreter
The interpreter mode in Rhino does not limit any longer the script size or code complexity. It should be possible to execute any script as long as JVM resources allow so.

See [Bugzilla 244014](https://bugzilla.mozilla.org/show_bug.cgi?id=244014) and [Bugzilla 256339](https://bugzilla.mozilla.org/show_bug.cgi?id=256339) for details.

### Tail call elimination in the interpreter
The interpreter mode in Rhino implements tail call elimination to avoid excessive stack space consumption when a function returns result of a call to another function.

See [Bugzilla 257128](https://bugzilla.mozilla.org/show_bug.cgi?id=257128)

### Support for continuations in the interpreter
The interpreter mode in Rhino supports continuations. The code is based on the ideas from the original implementation of continuations by Christopher Oliver and [SISC](http://sisc.sourceforge.net/) project. To use the continuations make sure that the interpreter mode is selected through [setting](https://javadoc.io/doc/org.mozilla/rhino/latest/org/mozilla/javascript/Context.html#setOptimizationLevel-int-) the optimization level to -1 or by adding `-opt -1` to the command line of [Rhino shell](../../_tools/shell.md).

Please note that the details of implementation and Java and JavaScript API for continuations may change in future in incompatible way.

See [Bugzilla 258844](https://bugzilla.mozilla.org/show_bug.cgi?id=258844)

### JavaImporter constructor
`JavaImporter` is a new global constructor that allows to omit explicit package names when scripting Java:
```js
var SwingGui = JavaImporter(Packages.javax.swing,
                            Packages.javax.swing.event,
                            Packages.javax.swing.border,
                            java.awt.event,
                            java.awt.Point,
                            java.awt.Rectangle,
                            java.awt.Dimension);
...

with (SwingGui) {
    var mybutton = new JButton(test);
    var mypoint = new Point(10, 10);
    var myframe = new JFrame();
...
}
```
Previously such functionality was available only to embeddings that used [org.mozilla.javascript.ImporterTopLevel](https://javadoc.io/doc/org.mozilla/rhino/latest/org/mozilla/javascript/ImporterTopLevel.html) class as the top level scope. The class provides additional `importPackage()` and `importClass()` global functions for scripts but their extensive usage has tendency to pollute the global name space with names of Java classes and prevents loaded classes from garbage collection.

See [Bugzilla 245882](https://bugzilla.mozilla.org/show_bug.cgi?id=245882) for details.

### Context customization API
[org.mozilla.javascript.ContextFactory](https://javadoc.io/doc/org.mozilla/rhino/latest/org/mozilla/javascript/ContextFactory.html) provides new API for customization of [org.mozilla.javascript.Context](https://javadoc.io/doc/org.mozilla/rhino/latest/org/mozilla/javascript/Context.html) and ensures that application-specific Context subclasses will always be used when Rhino runtime needs to create Context instances.
See [Bugzilla 245882](https://bugzilla.mozilla.org/show_bug.cgi?id=245882) for details.

### Support for Date.now()
`Date.now()` function which is a SpiderMonkey extension to ECMAScript standard is available now in Rhino. The function returns number of milliseconds passed since 1970-01-01 00:00:00 UTC.

### Removal of deprecated classes
The following classes that were deprecated in Rhino 1.5R5 are no longer available in Rhino 1.6R1:
- org.mozilla.javascript.ClassNameHelper
- org.mozilla.javascript.ClassRepository

See documentation for [org.mozilla.javascript.optimizer.ClassCompiler](https://javadoc.io/doc/org.mozilla/rhino/latest/org/mozilla/javascript/optimizer/ClassCompiler.html) that provides replacement for ClassNameHelper and ClassRepository.