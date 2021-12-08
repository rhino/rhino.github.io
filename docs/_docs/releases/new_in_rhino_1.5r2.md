---
title: New in Rhino 1.5R2
parent: Releases
nav_order: -2
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
This is a log of significant changes since the release of Rhino 1.5 Release 1.

## Graphical debugger
Thanks to a contribution by Christopher Oliver, Rhino now has a graphical debugger. See [Rhino Debugger](../../_tools/debugger.md) for more details.

## Footprint reductions
Igor Bukanov has provided a wealth of changes to reduce the number and size of objects required by Rhino. In particular, he introduced a new way to represent the built-in objects like Date and RegExp that reduces the amount of memory required and speeds up `Context.initStandardObjects`.

## Interpreted mode performance improvements
Igor Bukanov also made a number of improvements to interpreter mode performance.

## JS/CORBA Adapter
Matthias Radestock wrote a module that allows JavaScript code to interact with CORBA. See [jscorba](http://sourceforge.net/projects/jscorba) for more details.

## Directory restructuring and Ant buildfile
I've restructured the the Rhino directory and written an [Ant](http://jakarta.apache.org/ant/index.html) buildfile. This should make building easier and more consistent with other open source Java projects.

## FlattenedObject deprecated
I wrote FlattenedObject to provide a means for dealing with JavaScript objects in prototype chains. Where Scriptable defines the primitive operations, FlattenedObject defines the aggregate operations of manipulating properties that may be defined in an object or in an object reachable by a succession of getPrototype calls. However, I now believe that I designed FlattenedObject poorly. Perhaps it should have been a clue that I was never satisfied with the name: if it's hard to express the name of the object it may mean the function the object is supposed to fulfill is not well defined either. The problem is that it is inefficient since it requires an extra object creation, and balky because of that extra level of wrapping.

So I've checked in changes that deprecate FlattenedObject. I've introduced new static methods in ScriptableObject (thanks to beard@netscape.com for the idea) that replace the functionality. These methods perform the get, put, and delete operations on a Scriptable object passed in without the overhead of creating a new object.

## WrapHandler interface
Embeddings that wish to provide their own custom wrappings for Java objects may implement this interface and call Context.setWrapHandler. See WrapHandler javadoc.

## ClassOutput interface
An interface embedders can implement in order to control the placement of generated class bytecodes. See the javadoc.