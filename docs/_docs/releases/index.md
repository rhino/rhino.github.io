---
title: Releases
has_children: true
has_toc: false
---
# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Release Notes and zip files containing both the source code and a binary) are available from Rhino 1.4R3 onwards, which is the first public release.

As of Rhino 1.7R5 development and releases are done through the [Rhino repository](https://github.com/mozilla/rhino) on Github and through the [Releases section](https://github.com/mozilla/rhino/releases) on GitLab the assets can be downloaded separately:

## Available artifacts

|  Artifact  |  Description  |  Usage  |  Notes  |
|  `rhino-X.X.X.jar`  |  Full jar, including tools[^1], excluding the JSR-223 Script engine wrapper  |  Use when any of the tools[^1] are required. Otherwise use `rhino-runtime-X.X.X.jar` artifact  |    |
|  `rhino-engine-X.X.X.jar`  |  JSR-223 Script Engine wrapper  |  To be combined with either the `rhino-X.X.X.jar` or `rhino-runtime-X.X.X.jar` artifact when using Rhino through the Java Script Engine interface  |  [Available since Rhino 1.7.13](new_in_rhino_1.7.13.md/#script-engine-support)  |
|  `rhino-runtime-X.X.X.jar`  |  Stripped-down jar, excludes tools[^1]  |  Use for embedding scenario's that don't require any of the tools[^1]  |  [Available since Rhino 1.7.12](new_in_rhino_1.7.12.md#new-jar-for-embedding-use-cases)  |

Note: these are the currently available artifacts in the latest releases of Rhino. Historically other artifacts have been available.

## Release Overview

|  Release  |  Release Date  |  Change log  |  Download link  |
|  ---  |  ---  |  ---  |  ---  |
|  Rhino 1.7.13  |  2020-09-02  |  [Release Notes](new_in_rhino_1.7.13.md)  |  [rhino1.7.13.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_13_Release/rhino-1.7.13.zip)  |
|  Rhino 1.7.12  |  2020-01-13  |  [Release Notes](new_in_rhino_1.7.12.md)  |  [rhino1.7.12.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_12_Release/rhino-1.7.12.zip)  |
|  Rhino 1.7.11  |  2019-05-30  |  [Release Notes](new_in_rhino_1.7.11.md)  |  [rhino1.7.11.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_11_Release/rhino-1.7.11.zip)  |
|  Rhino 1.7.10  |  2018-04-09  |  [Release Notes](new_in_rhino_1.7.10.md)  |  [rhino1.7.10.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_10_Release/rhino-1.7.10.zip)  |
|  Rhino 1.7.9  |  2018-03-15  |  [Release Notes](new_in_rhino_1.7.9.md)  |  [rhino1.7.9.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_9_Release/rhino-1.7.9.zip)  |
|  Rhino 1.7.8  |  2018-01-22  |  [Release Notes](new_in_rhino_1.7.8.md)  |  [rhino1.7.8.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_8_Release/rhino-1.7.8.zip)  |
|  Rhino 1.7.7.2  |  2017-08-24  |  [Release Notes](new_in_rhino_1.7.7.2.md)  |  [rhino1.7.7.2.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_7_2_Release/rhino-1.7.7.2.zip)  |
|  Rhino 1.7.7.1  |  2016-02-01  |  [Release Notes](new_in_rhino_1.7.7.1.md)  |  [rhino1.7.7.1.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_7_1_RELEASE/rhino-1.7.7.1.zip)  |
|  Rhino 1.7.7  |  2015-06-17  |  [Release Notes](new_in_rhino_1.7.7.md)  |  [rhino1.7.7.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_7_RELEASE/rhino1.7.7.zip)  |
|  Rhino 1.7.6  |  2015-04-15  |  [Release Notes](new_in_rhino_1.7.6.md)  |  [rhino1.7.6.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_6_RELEASE/rhino1.7.6.zip)  |
|  Rhino 1.7R5  |  2015-01-29  |  [Release Notes](new_in_rhino_1.7r5.md)  |  [rhino1_7R5.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7R5_RELEASE/rhino1_7R5.zip)  |
|  Rhino 1.7R4  |  2012-06-18  |  [New in Rhino 1.7R4](new_in_rhino_1.7r4.md)  |  [rhino1_7R4.zip](https://github.com/downloads/mozilla/rhino/rhino1_7R4.zip)  |
|  Rhino 1.7R3  |  2011-05-09  |  [New in Rhino 1.7R3](new_in_rhino_1.7r3.md)  |  [rhino1_7R3.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_7R3.zip)  |
|  Rhino 1.7R2  |  2009-03-22  |  [New in Rhino 1.7R2](new_in_rhino_1.7r2.md)  |  [rhino1_7R2.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_7R2.zip)  |
|  Rhino 1.7R1  |  2008-03-06  |  [New in Rhino 1.7R1](new_in_rhino_1.7r1.md)  |  [rhino1_7R1.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_7R1.zip)  |
|  Rhino 1.6R7  |  2007-08-20  |  [New in Rhino 1.6R7](new_in_rhino_1.6r7.md)  |  [rhino1_6R7.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R7.zip)  |
|  Rhino 1.6R6[^2]  |  2007-07-30  |  [New in Rhino 1.6R6](new_in_rhino_1.6r6.md)  |  [rhino1_6R6.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R6.zip)  |
|  Rhino 1.6R5[^2]  |  2006-11-19  |  Same code as 1.6R4, but relicensed under MPL/GPL.  |  [rhino1_6R5.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R5.zip)  |
|  Rhino 1.6R4[^2]  |  2006-09-10  |  [bug 343976](https://bugzilla.mozilla.org/show_bug.cgi?id=343976)  |  [rhino1_6R4.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R4.zip)  |
|  Rhino 1.6R3[^2]  |  2006-07-24  |  [Changes in 1.6R3](new_in_rhino_1.6r3.md)  |  [rhino1_6R3.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R3.zip)  |
|  Rhino 1.6R2[^2]  |  2005-09-19  |  [Changes in 1.6R2](new_in_rhino_1.6r2.md)  |  [rhino1_6R2.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R2.zip)  |
|  Rhino 1.6R1[^2]  |  2004-11-29  |  [Changes in 1.6R1](new_in_rhino_1.6r1.md)  |  [rhino1_6R1.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R1.zip)  |
|  Rhino 1.5R5[^2]  |  2004-03-25  |  [Changes in 1.5R5](new_in_rhino_1.5r5.md)  |  [rhino1_5R5.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_5R5.zip)  |
|  Rhino 1.5R4.1  |  2003-04-21  |  [Changes in 1.5R4.1](new_in_rhino_1.5r4.1.md)  |  [rhino15R41.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino15R41.zip)  |
|  Rhino 1.5R4  |  2003-02-10  |  [Changes in 1.5R4](new_in_rhino_1.5r4.md)  |  [rhino15R4.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino15R4.zip)  |
|  Rhino 1.5R3  |  2002-01-27  |  [Changes in 1.5R3](new_in_rhino_1.5r3.md)  |  [rhino15R3.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino15R3.zip)  |
|  Rhino 1.5R2  |  2001-07-27  |  [Changes in 1.5R2](new_in_rhino_1.5r2.md)  |  [rhino15R2.zip](https://ftp.mozilla.org/pub/mozilla.org/js/older-packages/rhino15R2.zip)  |
|  Rhino 1.5R1  |  2000-09-10  |  [Changes in 1.5R1](new_in_rhino_1.5r1.md)  |  [rhino15R1.zip](https://ftp.mozilla.org/pub/mozilla.org/js/older-packages/rhino15R1.zip)  |
|  Rhino 1.4R3  |  1999-05-10  |  Initial public release  |  [rhino14R3.zip](https://ftp.mozilla.org/pub/mozilla.org/js/older-packages/rhino14R3.zip)  |


## Maven
Rhino is also available through [MVNnrepository](https://mvnrepository.com/)

```xml
<dependency>
    <groupId>org.mozilla</groupId>
    <artifactId>rhino</artifactId>
    <version>1.7.13</version>
</dependency>
```

---
[^1]: Rhino Tools consist of:
    - [Debugger](../../_tools/debugger.md): Visual, Swing-based Debugger for Rhino
    - [Shell](../../_tools/shell.md): Interactive JavaScript [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)
    - [JavaScript Compiler](../../_tools/javascript_compiler.md): Command-line Utility to compile JavaScript to Java Class files

    Note that some automated source-scanning tools mark these capabilties as insecure, hence the reason of providing the rhino-runtime-X.X.X.jar that excludes the tools

[^2]: Rhino 1.6R1 through 1.6R6 implements [E4X](https://developer.mozilla.org/en-US/docs/Archive/Web/E4X) using the [XMLBeans](https://xmlbeans.apache.org/) library.

    If you would like to use E4X you need to add `xbean.jar` from XMLBeans distribution to your class path.

    Rhino 1.6R6 and later the E4X support has been rewritten to rely solely on the DOM3 APIs supported natively by Java 1.5.

    Pre-Java 1.5 users can use DOM3 using Java's endorsed standards override mechanism if they have a DOM3-capable XML parser. 

    If neither XMLBeans nor DOM3 are present, E4X is not available.