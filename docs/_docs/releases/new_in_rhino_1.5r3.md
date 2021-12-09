---
title: New in Rhino 1.5R3
parent: Releases
nav_order: -3
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
This is a log of significant changes since the release of Rhino 1.5 Release 2.

## Serialization
See the [serialization documentation](../serialization.md).

## Class writer API changes
Courtesy of Kemal Bayram.

> The biggest change I've made is the replacement of ClassOutput with ClassRepository that has the single method:
> ```java
>     public boolean storeClass(String className, byte[] classBytes, boolean isTopLevel) throws IOException;
> ```
> This interface allows any arbitary storage method, such as a Hashtable/Map. In addition it also allows you to specify whether a class should be loaded, via returning true or false.  You can still use ClassOutput as I've coded an internal wrapper.
> 
> With this interface it has also been possible to strip out the file saving code from Codegen and OptClassNameHelper.  The file saving code is now an inner class FileClassRepository in Context. As a consequence of this  I've stripped out some methods from ClassNameHelper. The resulting code is much more cleaner then before hand and everything still works as per usual.
> 
> Other small additions are:
> - Annonymous functions are now named class$1 instead of class1
> - get/setClassName added to ClassNameHelper exposed in Context.