---
title: Rhino 1.7.7.1
parent: Releases
nav_order: 20.1
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
This release fixes a few critical bugs that were affecting code in the field:
- Improve String.prototype.repeat to work more efficiently and to not overflow
- Fix CallSite.isNative() and isTopLevel() so that they do not throw fatal errors
- Replace the implementation of the "YearFromTime" internal method for the Date class to avoid large CPU loops

Specific Changes:
- Formatting issue with SourceReader.
- Fix CallSite.isNative() and isTopLevel() to not throw.
- Make String.prototype.repeat not overflow for large values, and change code style a bit.
- Add tests from 1.7.7.
- Add Gradle code from 1.7.7.
- Replace YearFromTime with code from jsdate.cpp to avoid long CPU loops.
