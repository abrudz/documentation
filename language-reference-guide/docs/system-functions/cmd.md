---
search:
  exclude: true
---

# <span>Windows Processor</span> `⎕CMD`

`⎕CMD` passes a command to the Microsoft Windows Command Processor, starts a Windows program, or starts an auxiliary processor. The presence of a left argument chooses between the last of these and the other two.

`⎕CMD` and [`⎕SH`](sh.md) are synonyms: either name can be used on either platform, with exactly the same effect. What differs is the platform, not the name, so these pages describe Microsoft Windows and the [`⎕SH`](sh.md) pages describe Unix. `⎕CMD` is the more natural name for the Windows user.

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
