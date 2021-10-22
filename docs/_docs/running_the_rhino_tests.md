---
title: "Running the Rhino tests"
---
# Running the Rhino tests
{: .no_toc }

{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
To run the [Rhino](undefined.md) tests, simply run the `junit-all` Ant task in the top-level Rhino directory:

```
$ cd rhino
$ ant junit-all
```

This will run Rhino's own unit tests as well as most of the Mozilla JavaScript test suite.

Test results can be viewed in HTML format in file `build/test/report/index.html`.