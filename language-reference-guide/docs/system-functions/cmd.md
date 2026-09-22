---
search:
  exclude: true
---

# <span>Windows Processor</span> `⎕CMD`

`⎕CMD` passes a command to the Microsoft Windows Command Processor, starts a Windows program, or starts an auxiliary processor. The presence of a left argument chooses between the last of these and the other two.

`⎕CMD` is a synonym of [`⎕SH`](sh.md), which documents the same actions on Unix. Either name can be used on either platform, with the behaviour of the platform it runs on.

## Call Windows Command Processor

[Monadic `⎕CMD`](cmd-monadic.md) runs a command and returns its output, a line per element, or starts a program and returns immediately:

```apl
      ⍴⎕CMD'dir'
12
```

## Start Windows Auxiliary Processor

[Dyadic `⎕CMD`](cmd-dyadic.md) starts an auxiliary processor, defining external functions in the workspace:

```apl
      'xutils' ⎕CMD ''
      )FNS
avx     box     dbr     getenv  hex     ltom    ltov    mtol    ss      vtol
```
