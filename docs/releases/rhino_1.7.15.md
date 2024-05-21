---
title: Rhino 1.7.15
parent: Releases
nav_order: 28
---

# {{ page.title }}
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
# Links
* [1.7.14 milestone](https://github.com/mozilla/rhino/milestone/17)
* [All merged PRs](https://github.com/mozilla/rhino/pulls?q=is%3Apr+merged%3A2022-01-06..2024-05-05)

# Rhino 1.7.15

Highlights of this release include:

* Basic support for "rest parameters"
* Improvements in Unicode support
* "Symbol.species" implemented in many places
* More correct property ordering in many places
* And many more improvements and bug fixes

This release includes committs from 29 different committers. Thanks to you all for your help!

## What's Changed
* Prepare for 1.7.15 by @gbrail in https://github.com/mozilla/rhino/pull/1148
* Implements Promise.allSettled() by @grob in https://github.com/mozilla/rhino/pull/1090
* Fix issue #1041. Handles {0} quantifier with max of zero correctly. by @MaxisTekfield in https://github.com/mozilla/rhino/pull/1098
* Add proper import package instructions in the OSGi manifest by @makusuko in https://github.com/mozilla/rhino/pull/1163
* add Object.hasOwn (#1052) in https://github.com/mozilla/rhino/pull/1157
* Apply spotlessApply to all code by @tuchida in https://github.com/mozilla/rhino/pull/1159
* Remove spotless "ratchet" by @gbrail in https://github.com/mozilla/rhino/pull/1170
* unify and improve the error msg about unsupported regex flags by @rbri in https://github.com/mozilla/rhino/pull/1180
* implement regex sticky support by @rbri in https://github.com/mozilla/rhino/pull/1181
* Fix GitHub Languages for repo by @p-bakker in https://github.com/mozilla/rhino/pull/1185
* fix #780 fix Object.assign when undefined value and inextensible by @tuchida in https://github.com/mozilla/rhino/pull/1186
* fix #934 Implement ES2017 Object.getOwnPropertyDescriptors by @tuchida in https://github.com/mozilla/rhino/pull/1193
* code cleanup by @rbri in https://github.com/mozilla/rhino/pull/1196
* take the offset of the buffer into account when construction a subarray from a buffer (fixes #1204) by @rbri in https://github.com/mozilla/rhino/pull/1205
* Various fixed for NativeConsole by @rbri in https://github.com/mozilla/rhino/pull/1207
* more console fixes and tests by @rbri in https://github.com/mozilla/rhino/pull/1208
* two json stringify fixes by @rbri in https://github.com/mozilla/rhino/pull/1209
* fix for toLocaleLowercase parameter handling by @rbri in https://github.com/mozilla/rhino/pull/1131
* improve log output of Callable's by @rbri in https://github.com/mozilla/rhino/pull/1213
* Simplify release steps by @zloirock in https://github.com/mozilla/rhino/pull/1214
* Some cleanup and minor optimizations by @rbri in https://github.com/mozilla/rhino/pull/1212
* Fix typeof for native classes with shared global scope #1173 by @Schmidor in https://github.com/mozilla/rhino/pull/1211
* Make the $262 object available within the test262 tests by @p-bakker in https://github.com/mozilla/rhino/pull/1229
* Fix ClassCastException when using StringBuilder/Buffer #496 by @shelches in https://github.com/mozilla/rhino/pull/1210
* fix missing scope definition at some places by @rbri in https://github.com/mozilla/rhino/pull/1227
* fix: parent relationship in TaggedTemplateLiteral (#1238) by @kuzjka in https://github.com/mozilla/rhino/pull/1239
* Make getCharacterEncoding in UrlModuleSourceProvider protected by @midgleyc in https://github.com/mozilla/rhino/pull/1233
* fix(#1237): polyfill android `Map.putIfAbsent` by @naijun0403 in https://github.com/mozilla/rhino/pull/1252
* Add PGP_KEYS.txt by @gbrail in https://github.com/mozilla/rhino/pull/1263
* fix the error message in case the quantifier maximum (second value) is smaller than the minimum (first value) by @rbri in https://github.com/mozilla/rhino/pull/1260
* Fix hasOwnProperty on NativeJavaObject by @Schmidor in https://github.com/mozilla/rhino/pull/1255
* Update README.md by @wimjongman in https://github.com/mozilla/rhino/pull/1266
* Function prototype properties length and name are configurable (in ES6) by @rbri in https://github.com/mozilla/rhino/pull/1284
* cleanup as follow up of pr 1284 by @rbri in https://github.com/mozilla/rhino/pull/1285
* make sure the placeholder replacements is also done for ConsStrings by @rbri in https://github.com/mozilla/rhino/pull/1293
* Code Cleanup by @rbri in https://github.com/mozilla/rhino/pull/1295
* Fix the condition for isResourceChanged by @szegedi in https://github.com/mozilla/rhino/pull/1301
* fix name property for bound functions (see issue #1297) by @rbri in https://github.com/mozilla/rhino/pull/1298
* next try to fix issue #780 by @rbri in https://github.com/mozilla/rhino/pull/1294
* fix ScriptException when bound functions are called inside Promise.then() by @rbri in https://github.com/mozilla/rhino/pull/1287
* Preserving cause on rethrown exceptions by @rPraml in https://github.com/mozilla/rhino/pull/1286
* BUG: for X of javaList does not work properly in strict mode by @rPraml in https://github.com/mozilla/rhino/pull/1304
* use try-with-resource by @rbri in https://github.com/mozilla/rhino/pull/1306
* setter function (from property descriptor) has to convert the args by @rbri in https://github.com/mozilla/rhino/pull/1305
* Treat String, ConsString, Boolean, and Double as value types by @szegedi in https://github.com/mozilla/rhino/pull/1302
* ci: set minimal permissions on GitHub Workflows by @diogoteles08 in https://github.com/mozilla/rhino/pull/1311
* Test optimization levels by @rbri in https://github.com/mozilla/rhino/pull/1317
* more test method cleanup by @rbri in https://github.com/mozilla/rhino/pull/1320
* fix some warnings in the test code by @rbri in https://github.com/mozilla/rhino/pull/1325
* fix some warnings in the test code by @rbri in https://github.com/mozilla/rhino/pull/1326
* remove default parameter from compareArray.js by @rbri in https://github.com/mozilla/rhino/pull/1329
* Support ES2019 Array.prototype.flat by @midgleyc in https://github.com/mozilla/rhino/pull/1313
* some code cleanup for the array_flat pr by @rbri in https://github.com/mozilla/rhino/pull/1330
* Es2022 at method by @JohnBain in https://github.com/mozilla/rhino/pull/1289
* some code cleanup for array at support by @rbri in https://github.com/mozilla/rhino/pull/1331
* PropertyDescriptor fixes by @rbri in https://github.com/mozilla/rhino/pull/1324
* Remove CircleCI configuration by @gbrail in https://github.com/mozilla/rhino/pull/1335
* take care of eof when parsing templates (fixes #1337) by @rbri in https://github.com/mozilla/rhino/pull/1338
* Create Security Policy by @diogoteles08 in https://github.com/mozilla/rhino/pull/1328
* docs(readme): remove broken MDN link by @caugner in https://github.com/mozilla/rhino/pull/1340
* Fix some deprecation warnings by @gbrail in https://github.com/mozilla/rhino/pull/1343
* This PR fixes the issue of flush() by @nmondal in https://github.com/mozilla/rhino/pull/1358
* Symbol fixes by @rbri in https://github.com/mozilla/rhino/pull/1357
* special handling for NativeError instances when generating the console output by @rbri in https://github.com/mozilla/rhino/pull/1366
* Fix regressions introduced to debugger by @gbrail in https://github.com/mozilla/rhino/pull/1369
* Add some micro-benchmarks for property access by @gbrail in https://github.com/mozilla/rhino/pull/1370
* fix a missing array limit check by @rbri in https://github.com/mozilla/rhino/pull/1371
* fix some typos in Messages.properties by @rbri in https://github.com/mozilla/rhino/pull/1373
* Update SunSpider benchmarks by @gbrail in https://github.com/mozilla/rhino/pull/1375
* take care of SymbolKey before casting by @rbri in https://github.com/mozilla/rhino/pull/1377
* Support ES2019 Array.prototype.flatMap by @midgleyc in https://github.com/mozilla/rhino/pull/1372
* feat: update github action versions to 3 by @midgleyc in https://github.com/mozilla/rhino/pull/1379
* Stop IRFactory from inheriting Parser by @tuchida in https://github.com/mozilla/rhino/pull/1380
* Array.of has to use defineOwnProperty instead of set by @rbri in https://github.com/mozilla/rhino/pull/1381
* Support unicode codepoint escape by @tuchida in https://github.com/mozilla/rhino/pull/1383
* convert NativeMath and NativeJSON into a Lambda based ScriptableObject by @rbri in https://github.com/mozilla/rhino/pull/1384
* Use a different method to determine if we are on Java 11 by @gbrail in https://github.com/mozilla/rhino/pull/1385
* javascript 'Set' cannot handle wrapped java objects properly by @rPraml in https://github.com/mozilla/rhino/pull/1387
* Modified `DoctestsTest` to include optimization level by @andreabergia in https://github.com/mozilla/rhino/pull/1401
* Allow updating of `name` of a function, as required by the standard by @andreabergia in https://github.com/mozilla/rhino/pull/1398
* [StepSecurity] ci: Harden GitHub Actions by @step-security-bot in https://github.com/mozilla/rhino/pull/1405
* Create dependabot.yml by @diogoteles08 in https://github.com/mozilla/rhino/pull/1407
* Make handling of object indices more in line with the spec by @gbrail in https://github.com/mozilla/rhino/pull/1392
* Support hashbang by @p-bakker in https://github.com/mozilla/rhino/pull/1417
* Add Scorecard Action by @diogoteles08 in https://github.com/mozilla/rhino/pull/1400
* Adds support for trailing commas in function parameters by @p-bakker in https://github.com/mozilla/rhino/pull/1416
* Handle Array prototype properties in standard operations by @gbrail in https://github.com/mozilla/rhino/pull/1426
* limit the length of the string to be used for indentation by @rbri in https://github.com/mozilla/rhino/pull/1428
* BigIntLiteral.toSource includes suffix by @JohnCokerC3 in https://github.com/mozilla/rhino/pull/1432
* Fixes for Symbol.iterator handling in NativeArray by @rbri in https://github.com/mozilla/rhino/pull/1435
* fix clz32 rounding errors by @rbri in https://github.com/mozilla/rhino/pull/1430
* Various fixes and implementations to NativeRegExp by @rbri in https://github.com/mozilla/rhino/pull/1434
* Fix `Math.atanh` by @andreabergia in https://github.com/mozilla/rhino/pull/1438
* add @Override and some try-with-resources by @rbri in https://github.com/mozilla/rhino/pull/1449
* (Partial) implementation of `[Symbol.species]` by @andreabergia in https://github.com/mozilla/rhino/pull/1448
* add species support to typed arrays by @rbri in https://github.com/mozilla/rhino/pull/1454
* SpecialRef: fix assigning to Symbol.__proto__ returning undefined by @rbri in https://github.com/mozilla/rhino/pull/1457
* an optimized version of Context#close() by @rbri in https://github.com/mozilla/rhino/pull/1460
* fix: toString() on generator by @0xe in https://github.com/mozilla/rhino/pull/1462
* a bit cleanup for the PR by @rbri in https://github.com/mozilla/rhino/pull/1467
* Fixed handling of unicode characters in the lexer by @andreabergia in https://github.com/mozilla/rhino/pull/1464
* update scorecard workflow by @rbri in https://github.com/mozilla/rhino/pull/1468
* Make regexp execution loop interruptible #1189 by @blutorange in https://github.com/mozilla/rhino/pull/1440
* initial implementation of function rest parameter support by @rbri in https://github.com/mozilla/rhino/pull/1451
* Fix unhandled promise rejection handler after a `.then` by @andreabergia in https://github.com/mozilla/rhino/pull/1469
* Update files for 1.7.15 release by @gbrail in https://github.com/mozilla/rhino/pull/1471

## New Contributors
* @grob made their first contribution in https://github.com/mozilla/rhino/pull/1090
* @makusuko made their first contribution in https://github.com/mozilla/rhino/pull/1163
* @zloirock made their first contribution in https://github.com/mozilla/rhino/pull/1214
* @Schmidor made their first contribution in https://github.com/mozilla/rhino/pull/1211
* @shelches made their first contribution in https://github.com/mozilla/rhino/pull/1210
* @midgleyc made their first contribution in https://github.com/mozilla/rhino/pull/1233
* @naijun0403 made their first contribution in https://github.com/mozilla/rhino/pull/1252
* @wimjongman made their first contribution in https://github.com/mozilla/rhino/pull/1266
* @diogoteles08 made their first contribution in https://github.com/mozilla/rhino/pull/1311
* @JohnBain made their first contribution in https://github.com/mozilla/rhino/pull/1289
* @caugner made their first contribution in https://github.com/mozilla/rhino/pull/1340
* @nmondal made their first contribution in https://github.com/mozilla/rhino/pull/1358
* @andreabergia made their first contribution in https://github.com/mozilla/rhino/pull/1401
* @step-security-bot made their first contribution in https://github.com/mozilla/rhino/pull/1405
* @JohnCokerC3 made their first contribution in https://github.com/mozilla/rhino/pull/1432
* @0xe made their first contribution in https://github.com/mozilla/rhino/pull/1462
* @blutorange made their first contribution in https://github.com/mozilla/rhino/pull/1440

**Full Changelog**: https://github.com/mozilla/rhino/compare/Rhino1_7_14_Release...Rhino1_7_15_Release