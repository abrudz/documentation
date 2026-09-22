---
search:
  boost: 2
---

# <span>Call Unix Command Processor</span> `{R}←⎕SH Y`{{key}}

This function passes a command to the Unix shell and returns its output. To start an auxiliary processor instead, see [Start Unix Auxiliary Processor](sh-dyadic.md). For the behaviour of `⎕SH` and its synonym [`⎕CMD`](cmd.md) on Microsoft Windows, see [Call Windows Command Processor](cmd-monadic.md).

The system commands [`)SH`](../system-commands/sh.md) and [`)CMD`](../system-commands/cmd.md) provide similar facilities.

`Y` must be a simple character scalar or vector representing a UNIX shell command.  `R` is a nested vector of character vectors.

`Y` may be any acceptable UNIX command. If the command does not produce any output, `R` is `0⍴⊂''` but the result is [shy](../../programming-reference-guide/introduction/results.md#shy-results).  If the command has a non-zero exit code, then APL will signal a `DOMAIN ERROR`.  If the command returns a result and has a zero exit code, then each element of `R` will be a line from the standard output (stdout) of the command.  Output from standard error (stderr) is not captured unless redirected to stdout.

See also [`⎕SHELL`](shell.md).

<h2 class="example">Examples</h2>

```apl
      ⎕SH'ls'
FILES WS temp
 
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
