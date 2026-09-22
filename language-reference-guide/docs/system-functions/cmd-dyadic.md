---
search:
  boost: 2
---

# <span>Start Windows Auxiliary Processor</span> `{R}←X ⎕CMD Y`{{key}}

This function starts an auxiliary processor. To run a command instead, see [Call Windows Command Processor](cmd-monadic.md). As far as the workspace is concerned the effect is the same on both platforms, although the implementation differs; for Unix see [Start Unix Auxiliary Processor](sh-dyadic.md).

!!! Hint "Hints and Recommendations"
    Although it is still possible for users to create their own APs, Dyalog Ltd. strongly recommends creating shared libraries/DLLs instead.

`X` must be a simple character vector containing the name (or pathname) of a Dyalog APL Auxiliary Processor (AP).

`Y` may be a simple character scalar or vector, or a vector of character vectors.  Under Windows the contents of `Y` are ignored.

`⎕CMD` loads the Auxiliary Processor into memory.  If no other APs are currently running, `⎕CMD` also allocates an area of memory for communication between APL and its APs.

The [shy](../../programming-reference-guide/introduction/results.md#shy-results) result `R` is the process id of the Auxiliary Processor task.

The effect of starting an AP is that one or more **external functions** are defined in the workspace.  These appear as locked functions and may be used in exactly the same way as regular defined functions.

When an external function is used in an expression, the argument(s) (if any) are passed to the AP for processing via the communications area described above.  APL halts whilst the AP is processing, and waits for a result.  Under Windows, unlike under UNIX, it is not possible for external functions to run in parallel with APL.

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕CMD CMD
</div>
