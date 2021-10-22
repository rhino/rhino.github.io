---
title: "Downloads archive"
---
# Downloads archive
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
See also [Rhino downloads](download_rhino.md).

You can download binary distributions of Rhino from [http://ftp.mozilla.org/pub/mozilla.org/js/](https://ftp.mozilla.org/pub/mozilla.org/js/).

|  Release  |  Release Date  |  Change log  |  Download link  |
|  ---  |  ---  |  ---  |  ---  |
|  Rhino 1.7R4  |  2012-06-18  |  [New in Rhino 1.7R4](new_in_rhino_1.7r4.md)  |  [rhino1_7R4.zip](https://github.com/downloads/mozilla/rhino/rhino1_7R4.zip)  |
|  Rhino 1.7R3  |  2011-05-09  |  [New in Rhino 1.7R3](new_in_rhino_1.7r3.md)  |  [rhino1_7R3.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_7R3.zip)  |
|  Rhino 1.7R2  |  2009-03-22  |  [New in Rhino 1.7R2](new_in_rhino_1.7r2.md)  |  [rhino1_7R2.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_7R2.zip)  |
|  Rhino 1.7R1  |  2008-03-06  |  [New in Rhino 1.7R1](new_in_rhino_1.7r1.md)  |  [rhino1_7R1.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_7R1.zip)  |
|  Rhino 1.6R7  |  2007-08-20  |  [New in Rhino 1.6R7](new_in_rhino_1.6r7.md)  |  [rhino1_6R7.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R7.zip)  |
|  Rhino 1.6R6  |  2007-07-30  |  [New in Rhino 1.6R6](new_in_rhino_1.6r6.md)  |  [rhino1_6R6.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R6.zip)  |
|  Rhino 1.6R5  |  2006-11-19  |  Same code as 1.6R4, but relicensed under MPL/GPL.  |  [rhino1_6R5.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R5.zip)  |
|  Rhino 1.6R4  |  2006-09-10  |  [bug 343976](https://bugzilla.mozilla.org/show_bug.cgi?id=343976)  |  [rhino1_6R4.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R4.zip)  |
|  Rhino 1.6R3  |  2006-07-24  |  [Changes in 1.6R3](https://www-archive.mozilla.org/rhino/rhino16r3)  |  [rhino1_6R3.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R3.zip)  |
|  Rhino 1.6R2  |  2005-09-19  |  [Changes in 1.6R2](https://www-archive.mozilla.org/rhino/rhino16r2)  |  [rhino1_6R2.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R2.zip)  |
|  Rhino 1.6R1  |  2004-11-29  |  [Changes in 1.6R1](https://www-archive.mozilla.org/rhino/rhino16r1)  |  [rhino1_6R1.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_6R1.zip)  |
|  Rhino 1.5R5  |  2004-03-25  |  [Changes in 1.5R5](https://www-archive.mozilla.org/rhino/rhino15r5)  |  [rhino1_5R5.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino1_5R5.zip)  |
|  Rhino 1.5R4.1  |  2003-04-21  |  [Changes in 1.5R4.1](https://web.archive.org/web/20030609002716/http://www.mozilla.org/rhino/rhino15R41.html)  |  [rhino15R41.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino15R41.zip)  |
|  Rhino 1.5R4  |  2003-02-10  |  [Changes in 1.5R4](https://www-archive.mozilla.org/rhino/rhino15r4)  |  [rhino15R4.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino15R4.zip)  |
|  Rhino 1.5R3  |  2002-01-27  |  [Changes in 1.5R3](https://www-archive.mozilla.org/rhino/rhino15r3)  |  [rhino15R3.zip](https://ftp.mozilla.org/pub/mozilla.org/js/rhino15R3.zip)  |
|  Rhino 1.5R2  |  2001-07-27  |  [Changes in 1.5R2](https://www-archive.mozilla.org/rhino/rhino15r2)  |  [rhino15R2.zip](https://ftp.mozilla.org/pub/mozilla.org/js/older-packages/rhino15R2.zip)  |
|  Rhino 1.5R1  |  2000-09-10  |  [Changes in 1.5R1](https://www-archive.mozilla.org/rhino/rhino15r1)  |  [rhino15R1.zip](https://ftp.mozilla.org/pub/mozilla.org/js/older-packages/rhino15R1.zip)  |
|  Rhino 1.4R3  |  1999-05-10  |  Initial public release  |  [rhino14R3.zip](https://ftp.mozilla.org/pub/mozilla.org/js/older-packages/rhino14R3.zip)  |

`Rhino 1.6R1 through 1.6R6 implement`[`E4X`](https://developer.mozilla.org/en-US/docs/Archive/Web/E4X)`using`[`XMLBeans`](https://xmlbeans.apache.org/)library. If you would like to use E4X you need to add `xbean.jar` from XMLBeans distribution to your class path. In Rhino 1.6R6 and later the E4X support has been rewritten to rely solely on the DOM3 APIs supported natively by Java 1.5. (Pre-Java 1.5 users can use DOM3 using Java's endorsed standards override mechanism if they have a DOM3-capable XML parser.) If neither XMLBeans nor DOM3 are present, E4X is not available.

If you are looking for `js.jar` for XSLT or for IBM's Bean Scripting Framework (BSF), please read the following [note](https://www.mozilla.org/rhino/bsf.html#bsf-issue) and then download one of the zip files above and unzip it.