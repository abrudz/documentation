---
search:
  boost: 2
---

# <span>Start Windows Auxiliary Processor</span> `{R}←X ⎕CMD Y`{{key}}

This function starts an auxiliary processor (AP). To run a command instead, see [Call Windows Command Processor](cmd-monadic.md). As far as the workspace is concerned the effect is the same on both platforms, although the implementation differs; for Unix see [Start Unix Auxiliary Processor](sh-dyadic.md).

<h2 class="example">Example</h2>

```apl
      'xutils' ⎕CMD ''
      )FNS
avx     box     dbr     getenv  hex     ltom    ltov    mtol    ss      vtol
```

!!! Hint "Hints and Recommendations"
    Although it is still possible for users to create their own APs, Dyalog Ltd. strongly recommends creating shared libraries/DLLs instead.

## Left Argument

`X` is a simple character vector containing the name, or pathname, of a Dyalog APL auxiliary processor.

## Right Argument

`Y` is a simple character scalar or vector, or a vector of character vectors. Its contents are ignored on Microsoft Windows.

## Result

The [shy](../../programming-reference-guide/introduction/results.md#shy-results) result `R` is the process id of the auxiliary processor task.

`⎕CMD` loads the auxiliary processor into memory. If no other APs are currently running, `⎕CMD` also allocates an area of memory for communication between APL and its APs.

## External Functions

Starting an AP defines one or more **external functions** in the workspace. These appear as locked functions and can be used in exactly the same way as regular defined functions.

When an external function is used in an expression, its arguments, if any, are passed to the AP for processing through the communications area described above. APL halts while the AP is processing and waits for a result. On Microsoft Windows, unlike on Unix, external functions cannot run in parallel with APL.

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕CMD CMD
</div>
