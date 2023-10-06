---
title: Rhino 1.7.7.2
parent: Releases
nav_order: 20.2
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
This release contains fixes for a few important bugs that have caught Rhino users out in the field.

- Do not throw a Java exception from array.prototype.sort() no matter how weird the user-supplied comparator function is. This is a major difference between JavaScript and Java and has caused us to avoid using "Arrays.sort" on JavaScript arrays.
- Fix incorrect offsets in the "DataView" class.

It also includes several other fixes:

- Always append a column number to V8-style stack traces. (Unfortunately it is always "0".)
- Support Object.is and Object.assign.
- Make the Symbol implementation match the spec (for VERSION_ES6 and up only).
- Avoid throwing internal Java exceptions for certain native objects in "toJSON".
- Allow subclassing of ContinuationPending.
- For VERSION_ES6 and up, sort properties in the spec-defined order (int property names first).
- Fix stack overflow in string concatenation.
- Improve performance of ConsString.toString

The next release is likely to be 1.7.8.