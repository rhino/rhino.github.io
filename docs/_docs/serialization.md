---
title: "Serialization"
---
# Serialization
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Beginning with Rhino 1.5 Release 3 it is possible to serialize JavaScript objects, including functions and scripts. However, serialization of code in compilation mode has some significant limitations. Serialization provides a way to save the state of an object and write it out to a file or send it across a network connection.

## Simple serialization example

The Rhino shell has two new top-level functions, serialize and deserialize. They're intended mainly as examples of the use of serialization:

```
`$``java org.mozilla.javascript.tools.shell.Main``js>``function f() { return 3; }``js>``serialize(f, "f.ser")``js>``quit()``$``java org.mozilla.javascript.tools.shell.Main``js>``f = deserialize("f.ser")``function f() {
    return 3;
}``js>``f()``3``js>`
```

Here we see a simple case of a function being serialized to a file and then read into a new instance of Rhino and called.

## Rhino serialization APIs

Two new classes, `ScriptableOutputStream` and `ScriptableInputStream`, were introduced to handle serialization of Rhino classes. These classes extend `ObjectOutputStream` and `ObjectInputStream` respectively. Writing an object to a file can be done in a few lines of Java code:

```
`FileOutputStream fos = new FileOutputStream(filename);``ScriptableOutputStream out = new ScriptableOutputStream(fos, scope);``out.writeObject(obj);``out.close();`
```

Here _filename_ is the file to write to, _obj_ is the object or function to write, and _scope_ is the top-level scope containing _obj_.

Reading the serialized object back into memory is similarly simple:

```
`FileInputStream fis = new FileInputStream(filename);``ObjectInputStream in = new ScriptableInputStream(fis, scope);``Object deserialized = in.readObject();``in.close();`
```

Again, we need the scope to create our serialization stream class.

So why do we need these specialized stream classes instead of simply using `ObjectOutputStream` and `ObjectInputStream`? To understand the answer we must know what goes on behind the scenes when Rhino serializes objects.

## How Rhino serialization works

By default, Java serialization of an object also serializes objects that are referred to by that object. Upon deserialization the initial object and the objects it refers to are all created and the references between the objects are resolved.

However, for JavaScript this creates a problem. JavaScript objects contain references to prototypes and to parent scopes. Default serialization would serialize the object or function we desired but would also serialize `Object.prototype` or even possibly the entire top-level scope and everything it refers to! We want to be able to serialize a JavaScript object and then deserialize it into a new scope and have all of the references from the deserialized object to prototypes and parent scopes resolved correctly to refer to objects in the new scope.

`ScriptableOutputStream` takes a scope as a parameter to its constructor. If in the process of serialization it encounters a reference to the scope it will serialize a marker that will be resolved to the new scope upon deserialization. It is also possible to add names of objects to a list in the `ScriptableOutputStream` object. These objects will also be saved as markers upon serialization and resolved in the new scope upon deserialization. Use the addExcludedName method of `ScriptableOutputStream` to add new names. By default, `ScriptableOutputStream` excludes all the names defined using `Context.initStandardObjects`.

If you are using Rhino serialization in an environment where you always define, say, a constructor _Foo_, you should add the following code before calling `writeObject`:

```
`out.addExcludedName("Foo");``out.addExcludedName("Foo.prototype");`
```

This code will prevent `Foo` and `Foo.prototype` from being serialized and will cause references to `Foo` or `Foo.prototype` to be resolved to the objects in the new scope upon deserialization. Exceptions will be thrown if `Foo` or `Foo.prototype` cannot be found the scopes used in either `ScriptableOutputStream` or `ScriptableInputStream`.

## Rhino serialization in compilation mode

Serialization works well with objects and with functions and scripts in interpretive mode. However, you can run into problems with serialization of compiled functions and scripts:

```
`$``cat test.js
`function f() { return 3; }
 serialize(f, "f.ser");
 g = deserialize("f.ser");
 print(g());` `$``java org.mozilla.javascript.tools.shell.Main -opt -1
test.js` 3 `$``java org.mozilla.javascript.tools.shell.Main test.js` `js: uncaught JavaScript exception: java.lang.ClassNotFoundException:
c1``
```

The problem is that Java serialization has no built-in way to serialize Java classes themselves. (It might be possible to save the Java bytecodes in an array and then load the class upon deserialization, but at best that would eat up a lot of memory for just this feature.) One way around this is to compile the functions using the jsc tool:

```
`$``cat f.js``function f() { return 3; }``$``java -classpath js.jar
org.mozilla.javascript.tools.jsc.Main f.js``$``cat test2.js``loadClass("f");
 serialize(f, "f.ser");
 g = deserialize("f.ser");
 print(g());``$``java -classpath 'js.jar;.'
org.mozilla.javascript.tools.shell.Main test2.js``3`
```

Now the function _f_ is compiled to a Java class, but that class is then made available in the classpath so serialization works. This isn't that interesting an example since compiling a function to a class and then loading it accomplishes the same as serializing an interpreted function, but it becomes more relevant if you wish to serialize JavaScript objects that have references to compiled functions.

## Original Document Information- Author: [Norris Boyd](mailto:norrisboyd@gmail.com)
- Last Updated Date: November 15, 2006
- Copyright Information: Portions of this content are © 1998–2006 by individual mozilla.org contributors; content available under a Creative Commons license | [Details](https://www.mozilla.org/foundation/licensing/website-content.html).