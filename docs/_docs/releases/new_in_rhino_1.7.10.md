---
title: New in Rhino 1.7.10
parent: Releases
nav_order: -23
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
(Note: This release is from April, 2018 -- I failed to update the GitHub release notes for it until 2019.)

This release fixes a regression introduced in version 1.7.7.2 that caused the
"propertyIsEnumerable" to throw an exception when used with String and typed array objects,
and possibly with custom user-written objects as well.

[Issue 415](https://github.com/mozilla/rhino/issues/415)

It contains a few other fixes:

Attila Szegedi (2):
- Make as many CallFrame fields as possible final, initialize them in constructor
- frame.debuggerFrame != null || frame.idata.itsNeedActivation is identical to frame.useActivation.

Jeremy Whitlock (1):
- Missing properties are not enumerable when checking enumerability