---
title: "FAQ"
---
# FAQ
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
#### Frequently Asked Questions about Rhino

## How do I create a Java array from JavaScript?

You must use Java reflection. For instance, to create an array of java.lang.String of length five, do

```
var stringArray = java.lang.reflect.Array.newInstance(java.lang.String, 5);
```

Then if you wish to assign the string "hi" to the first element, simply execute `stringArray[0] = "hi"`. Creating arrays of primitive types is slightly different: you must use the TYPE field. For example, creating an array of seven ints can be done with the code

```
var intArray = java.lang.reflect.Array.newInstance(java.lang.Integer.TYPE, 7);
```

## When I try to execute a script I get the exception `Required security context missing`. What's going on?

You've likely missed placing the `Security.properties` file in your class path at `org.mozilla.javascript.resources`.

## Can I use Rhino in a web browser?

Rhino is a library for Java use, and not for general web browsers. However, a Java-based browser may use Rhino with scripts from a page in the same manner that any other Java program would.