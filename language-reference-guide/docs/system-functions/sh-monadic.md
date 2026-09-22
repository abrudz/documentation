---
search:
  boost: 2
---

# <span>Call Unix Command Processor</span> `{R}←⎕SH Y`{{key}}

This function passes a command to the Unix shell and returns its output. To start an auxiliary processor instead, see [Start Unix Auxiliary Processor](sh-dyadic.md).

<h2 class="example">Example</h2>

```apl
      z←⎕SH'ls'
      z
┌─────┬────┬──┐
│FILES│temp│WS│
└─────┴────┴──┘
```

The system command [`)SH`](../system-commands/sh.md) provides a similar facility. A newer system function, [`⎕SHELL`](shell.md), can be used instead: it runs a program directly as well as through a shell, collects standard output and standard error separately, supplies input, sets the working directory and environment, imposes a timeout, and reports how the program ended rather than signalling `DOMAIN ERROR`.

## Right Argument

`Y` is a simple character scalar or vector containing a Unix shell command.

## Result

`R` is a vector of character vectors, each element a line of the command's standard output. Output to standard error is not captured unless redirected to standard output.

If the command produces no output, `R` is `0⍴⊂''` and is [shy](../../programming-reference-guide/introduction/results.md#shy-results). If the command has a non-zero exit code, `⎕SH` signals `DOMAIN ERROR`.

<h2 class="example">Examples</h2>

```apl
      ⎕SH 'rm WS/TEST'

      ⎕SH 'grep bin /etc/passwd ; exit 0'
bin:!:2:2::/bin:

      ⎕SH 'apl MYWS <inputfile >out1 2>out2 &'
```

!!! Info "Information"
    This function is disabled and instead generates a `DOMAIN ERROR` if the RIDE_SPAWNED parameter is non-zero. This is designed to prevent it being invoked from a Ride session which does not support this type of user interface. For further details, see the [Ride User Guide](https://dyalog.github.io/ride).

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕SH SH
</div>
