---
title: "Download Rhino"
---
# Download Rhino
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Rhino is available for download both in source and compiled form.

## Binaries

|  Release  |  Release Date  |  Change log  |  Download link  |
|  ---  |  ---  |  ---  |  ---  |
|  Rhino 1.7R4  |  2012-06-18  |  [New in Rhino 1.7R4](new_in_rhino_1.7r4.md)  |  [rhino1_7R4.zip](https://github.com/downloads/mozilla/rhino/rhino1_7R4.zip)  |
|  Rhino 1.7R5  |  2015-01-29  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7R5_RELEASE)  |  [rhino1_7R5.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7R5_RELEASE/rhino1_7R5.zip)  |
|  Rhino 1.7.6  |  2015-04-15  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_6_RELEASE)  |  [rhino1.7.6.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_6_RELEASE/rhino1.7.6.zip)  |
|  Rhino 1.7.7  |  2015-06-17  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_7_RELEASE)  |  [rhino1.7.7.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_7_RELEASE/rhino1.7.7.zip)  |
|  Rhino 1.7.7.1  |  2016-02-01  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_7_1_RELEASE)  |  [rhino1.7.7.1.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_7_1_RELEASE/rhino-1.7.7.1.zip)  |
|  Rhino 1.7.7.2  |  2017-08-24  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_7_2_Release)  |  [rhino1.7.7.2.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_7_2_Release/rhino-1.7.7.2.zip)  |
|  Rhino 1.7.8  |  2018-01-22  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_8_Release)  |  [rhino1.7.8.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_8_Release/rhino-1.7.8.zip)  |
|  Rhino 1.7.9  |  2018-03-15  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_9_Release)  |  [rhino1.7.9.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_9_Release/rhino-1.7.9.zip)  |
|  Rhino 1.7.10  |  2018-04-09  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_10_Release)  |  [rhino1.7.10.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_10_Release/rhino-1.7.10.zip)  |
|  Rhino 1.7.11  |  2019-05-30  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_11_Release)  |  [rhino1.7.11.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_11_Release/rhino-1.7.11.zip)  |
|  Rhino 1.7.12  |  2020-01-13  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_12_Release)  |  [rhino1.7.12.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_12_Release/rhino-1.7.12.zip)  |
|  Rhino 1.7.13  |  2020-09-02  |  [Release Notes](https://github.com/mozilla/rhino/releases/tag/Rhino1_7_13_Release)  |  [rhino1.7.13.zip](https://github.com/mozilla/rhino/releases/download/Rhino1_7_13_Release/rhino-1.7.13.zip)  |

To download older Rhino versions, see the [Rhino downloads archive.](rhino_downloads_archive.md)

## License

Rhino is open source. As of release 1.7R4 Rhino is available under [MPL](https://www.mozilla.org/MPL/) 2.0.

Previous versions were released under MPL 1.1/GPL 2.0 license.

See [Rhino license](license.md) for further information.

## Source

In addition to getting the source from the zip files above, the source code for Rhino can be found in github at [https://github.com/mozilla/rhino](https://github.com/mozilla/rhino). To get the source, use the command

```
git clone https://github.com/mozilla/rhino.git
```

Rhino uses Gradle as its build system. Running the `./gradlew tasks` command at the top directory of the Rhino distribution will print the list of available build targets.