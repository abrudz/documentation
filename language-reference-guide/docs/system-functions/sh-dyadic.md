---
search:
  boost: 2
---

# <span>Start Unix Auxiliary Processor</span> `{R}←X ⎕SH Y`{{key}}

This function starts an auxiliary processor (AP). To run a shell command instead, see [Call Unix Command Processor](sh-monadic.md). As far as the workspace is concerned the effect is the same on both platforms, although the implementation differs; for Microsoft Windows see [Start Windows Auxiliary Processor](cmd-dyadic.md).

<h2 class="example">Example</h2>

```apl
      'xutils' ⎕SH 'xutils' 'ss' 'dbr'
      )FNS
avx     box     dbr     getenv  hex     ltom    ltov    mtol    ss      vtol
```

!!! Hint "Hints and Recommendations"
    Although it is still possible for users to create their own APs, Dyalog Ltd. strongly recommends creating shared libraries/DLLs instead.

## Left Argument

`X` is a simple character vector naming the auxiliary processor to run. `⎕SH` loads it from that file, using a search path defined by the environment variable `WSPATH`.

## Right Argument

`Y` is a simple character scalar or vector, or a vector of character vectors, holding the parameters to pass to the auxiliary processor.

The syntax is similar to the Unix `execl(2)` system call, where `taskname` names the auxiliary processor to be executed and `arg0` through `argn` are the parameters of the calling line to be passed to the task:

```apl
      'taskname' ⎕SH 'arg0' 'arg1' ... 'argn'
```

## Result

The [shy](../../programming-reference-guide/introduction/results.md#shy-results) result `R` is the process id of the auxiliary processor task.

## External Functions

Starting an AP defines one or more **external functions** in the workspace. These appear as locked functions and can be used in exactly the same way as regular defined functions.

When an external function is used in an expression, its arguments, if any, are **piped** to the AP for processing. If the function returns a result, APL halts while the AP is processing and waits for the result. If not, it continues processing in parallel.

<h2 class="example">Example</h2>

```apl
      '/bin/sh' ⎕SH 'sh' '-c' 'adb test'
```

!!! Warning "Warning"
    Under macOS and Linux, if the configuration parameter **ENABLE_CEF** is 1, Auxiliary Processors cannot be used (they hang on error). The default value is 1 unless you are not running under a desktop (for example, you are running Dyalog in a PuTTY session when the default is 0).

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕SH SH
</div>
