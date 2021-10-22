---
title: "Requirements and limitations"
---
# Requirements and limitations
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## Requirements

Recent versions of Rhino have only been tested with JDK 1.4 and greater. Older versions support JDKs as early as 1.1.

To use the JavaAdapter feature or an optimization level of 0 or greater, Rhino must be running under a security manager that allows the definition of class loaders.

## Limitations

### LiveConnect

If a JavaObject's field's name collides with that of a method, the value of that field is retrieved lazily, and can be counter-intuitively affected by later assignments:

```
javaObj.fieldAndMethod = 5;
var field = javaObj.fieldAndMethod;
javaObj.fieldAndMethod = 7;
// now, field == 7
```

You can work around this by forcing the field value to be converted to a JavaScript type when you take its value:

```
javaObj.fieldAndMethod = 5;
var field = javaObj.fieldAndMethod + 0; // force conversion now
javaObj.fieldAndMethod = 7;
// now, field == 5
```

### JSObject

Rhino does **NOT** support the `netscape.javascript.JSObject` class.