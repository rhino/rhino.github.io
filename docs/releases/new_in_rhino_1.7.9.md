---
title: Rhino 1.7.9
parent: Releases
nav_order: -22
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
This release fixes a [potential ArrayIndexOutOfBoundsException](https://github.com/mozilla/rhino/issues/390) that was introduced in 1.7.8. Since it's potentially pretty serious, projects currently using 1.7.8 should switch to this new release.


In addition:

## [#398](https://github.com/mozilla/rhino/pull/398)
There is a new flag on Context called "FEATURE_INTEGER_WITHOUT_DECIMAL_PLACE." If set, Rhino will work harder to display numbers in integer form rather than in floating-point form. This feature is currently disabled by default, although if it proves popular than we can consider enabling it in the future.

## [#383](https://github.com/mozilla/rhino/pull/383)
At language level "ES6" and above, ToNumber conversion is now more compliant to the spec. (This change is disabled for older language levels to prevent a problem with backward compatibility.)

## Finally, there are a number of other fixes.

Thanks to all who contributed, both with issues and with code!

Attila Szegedi:
- Fix a JavaDoc warning

Ivan Vyshnevskyi:
- Make ToNumber(String) conversion more spec-compliant
- Report parsing error for default values in destructuring assignments

Michael[tm] Smith:
- Add addError(String messageId, int c) method
- Add “illegal character” test to ParserTest
- Show word in “identifier is a reserved word” error
- Add “identifier is a reserved word” test

Oleksandr Maksymenko:
- changes to process integer object as integer and long as long, not as double

RBRi:
- cleanup the code an try to make it faster [#373](https://github.com/mozilla/rhino/issues/373)

jhertel:
- Correction: Compatability → Compatibility