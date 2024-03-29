---
title: Rhino 1.7.7
parent: Releases
nav_order: 20
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
Major changes in this release: [Release 1.7.7](https://github.com/mozilla/rhino/issues?q=milestone%3A%22Release+1.7.7%22+is%3Aclosed)

Specific changes:
- [#202](https://github.com/mozilla/rhino/issues/202) Initial support for ECMA Script 6 "method definitions".
- [#201](https://github.com/mozilla/rhino/issues/201) Make sure that all native Error instances can be converted to JSON.
- [#184](https://github.com/mozilla/rhino/issues/184) Fix compile encoding errors.
- [#178](https://github.com/mozilla/rhino/issues/178) Support build using Gradle (build using Ant is still supported but will be removed in a future release.)
- [#176](https://github.com/mozilla/rhino/issues/176) Add ScriptRuntime.throwCustomError to make it easier to re-throw Java exceptions
- [#166](https://github.com/mozilla/rhino/issues/166) Support many ES6 additions to the Math class.
- [#165](https://github.com/mozilla/rhino/issues/165) Support many ES6 additions to the Number class.
- [#163](https://github.com/mozilla/rhino/issues/163) Support ES6 additions to the String class.

Thanks to everyone who contributed!
