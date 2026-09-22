---
search:
  exclude: true
---

# <span>Unix Processor</span> `⎕SH`

`⎕SH` passes a command to the Unix shell, or starts an auxiliary processor. The presence of a left argument chooses which.

`⎕SH` and [`⎕CMD`](cmd.md) are synonyms: either name can be used on either platform, with exactly the same effect. What differs is the platform, not the name, so these pages describe Unix and the [`⎕CMD`](cmd.md) pages describe Microsoft Windows. `⎕SH` is the more natural name for the Unix user.

## Call Unix Command Processor

[Monadic `⎕SH`](sh-monadic.md) runs a shell command and returns its output, a line per element:

```apl
      z←⎕SH'ls'
      z
┌─────┬────┬──┐
│FILES│temp│WS│
└─────┴────┴──┘
```

## Start Unix Auxiliary Processor

[Dyadic `⎕SH`](sh-dyadic.md) starts an auxiliary processor, defining external functions in the workspace:

```apl
      'xutils' ⎕SH 'xutils'
      )FNS
avx     box     dbr     getenv  hex     ltom    ltov    mtol    ss      vtol
```
