---
title: Rhino 1.6R2
parent: Releases
nav_order: 8
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Release Date: 2005-09-19

Rhino 1.6R2 is a new maintenance release of Rhino. New to Rhino 1.6Rx is support for ECMAScript for XML (E4X). See [Change Log for Rhino 1.6R1](new_in_rhino_1.6r1.md) for more details.

Bugs marked fixed in Rhino 1.6R2 ([query](https://bugzilla.mozilla.org/buglist.cgi?query_format=advanced&short_desc_type=allwordssubstr&short_desc=&product=Rhino%20Graveyard&long_desc_type=substring&long_desc=&bug_file_loc_type=allwordssubstr&bug_file_loc=&status_whiteboard_type=allwordssubstr&status_whiteboard=&keywords_type=allwords&keywords=&resolution=FIXED&emailassigned_to1=1&emailtype1=exact&email1=&emailassigned_to2=1&emailreporter2=1&emailqa_contact2=1&emailtype2=exact&email2=&bugidtype=include&bug_id=&votes=&chfieldfrom=2004-11-29&chfieldto=2005-08-21&chfield=resolution&chfieldvalue=FIXED&cmdtype=doit&order=Reuse+same+sort+as+last+time&field0-0-0=noop&type0-0-0=noop&value0-0-0=))
- [238649](https://bugzilla.mozilla.org/show_bug.cgi?id=238649) Removal of deprecated features after 1.5R5
- [243057](https://bugzilla.mozilla.org/show_bug.cgi?id=243057) enhancement - ability to assign to Java function result a...
- [252122](https://bugzilla.mozilla.org/show_bug.cgi?id=252122) double expansion of error message
- [255595](https://bugzilla.mozilla.org/show_bug.cgi?id=255595) Factory class for Context creation
- [258844](https://bugzilla.mozilla.org/show_bug.cgi?id=258844) Continuation support in interpreter
- [264637](https://bugzilla.mozilla.org/show_bug.cgi?id=264637) InterpretedFunction memory footprint could be lighter
- [271401](https://bugzilla.mozilla.org/show_bug.cgi?id=271401) JS prototypes for superclasses with ScriptableObject.defi...
- [274467](https://bugzilla.mozilla.org/show_bug.cgi?id=274467) Add JavaScript stack trace to exceptions
- [274996](https://bugzilla.mozilla.org/show_bug.cgi?id=274996) Exceptions with multiple interpreters on stack may lead t...
- [277537](https://bugzilla.mozilla.org/show_bug.cgi?id=277537) isXMLName() should be properly implemented
- [277935](https://bugzilla.mozilla.org/show_bug.cgi?id=277935) Assignments to descendants like "msg..s = something" => f...
- [278701](https://bugzilla.mozilla.org/show_bug.cgi?id=278701) Minimised windows don't indicate that breakpoints have be...
- [280047](https://bugzilla.mozilla.org/show_bug.cgi?id=280047) Not implementing Scriptable in Undefined
- [280629](https://bugzilla.mozilla.org/show_bug.cgi?id=280629) When using the debugger within another program the only w...
- [281067](https://bugzilla.mozilla.org/show_bug.cgi?id=281067)  ThreadLocal in Context prevents class unloading
- [281247](https://bugzilla.mozilla.org/show_bug.cgi?id=281247) JDK compatibility via special class
- [281537](https://bugzilla.mozilla.org/show_bug.cgi?id=281537) ScriptRuntime.toNumber warns on Undefined
- [282447](https://bugzilla.mozilla.org/show_bug.cgi?id=282447) NPE trying to report error when trying to convert null to...
- [282595](https://bugzilla.mozilla.org/show_bug.cgi?id=282595) Patch for BeanProperties to work with several setters for...
- [286251](https://bugzilla.mozilla.org/show_bug.cgi?id=286251) initFunction can be called twice
- [289294](https://bugzilla.mozilla.org/show_bug.cgi?id=289294) Infinite loop during a script compilation
- [289603](https://bugzilla.mozilla.org/show_bug.cgi?id=289603) Update rhino-n.tests to eliminate spidermonkey only tests
- [290034](https://bugzilla.mozilla.org/show_bug.cgi?id=290034) Cannot catch in JavaScript the original exception thrown ...
- [291591](https://bugzilla.mozilla.org/show_bug.cgi?id=291591) Rhino has differing behaviour to spidermonkey, and does n...
- [292324](https://bugzilla.mozilla.org/show_bug.cgi?id=292324) ArrayIndexOutOfBoundsException while compiling a script
- [298786](https://bugzilla.mozilla.org/show_bug.cgi?id=298786) Infinite loop when compiling with optimization
- [299539](https://bugzilla.mozilla.org/show_bug.cgi?id=299539) Bad bytecode for function assignments
- [299613](https://bugzilla.mozilla.org/show_bug.cgi?id=299613) Runtime support for function-results-as-lvalue
- [302501](https://bugzilla.mozilla.org/show_bug.cgi?id=302501) constructor property shouldn't be readonly
- [303572](https://bugzilla.mozilla.org/show_bug.cgi?id=303572) Need access to underlying RhinoException in rethrown erro...
- [305323](https://bugzilla.mozilla.org/show_bug.cgi?id=305323) Rhino fails to select the appropriate overloaded method
- [305753](https://bugzilla.mozilla.org/show_bug.cgi?id=305753) NativeJavaMethod objects have incorrect parent when using...
- [306258](https://bugzilla.mozilla.org/show_bug.cgi?id=306258) Can not compile using Ant scripts under JDK 1.5
- [306268](https://bugzilla.mozilla.org/show_bug.cgi?id=306268) Decompilation of E4X dot query is broken
- [306308](https://bugzilla.mozilla.org/show_bug.cgi?id=306308) JS function as Java interface via reflect.Proxy
- [306419](https://bugzilla.mozilla.org/show_bug.cgi?id=306419) Add serialVersionUID to Serializable
- [306584](https://bugzilla.mozilla.org/show_bug.cgi?id=306584) Crashes parsing .jsp page with javascripts
- [303460](https://bugzilla.mozilla.org/show_bug.cgi?id=303460) Enhance Rhino's shell to execute compiled script .class f...
- [306825](https://bugzilla.mozilla.org/show_bug.cgi?id=306825) Allow to use shell.Global in servlets
- [309029](https://bugzilla.mozilla.org/show_bug.cgi?id=309029) Exception when evaluating recursive function