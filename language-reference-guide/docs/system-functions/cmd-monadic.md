---
search:
  boost: 2
---

# <span>Call Windows Command Processor</span> `{R}←⎕CMD Y`{{key}}

This function passes a command to the Microsoft Windows Command Processor and returns its output, or starts a Windows program. To start an auxiliary processor instead, see [Start Windows Auxiliary Processor](cmd-dyadic.md).

<h2 class="example">Example</h2>

```apl
      Z←⎕CMD'dir'
      ⍴Z
12
      ↑Z
 Volume in drive C is OS
 Volume Serial Number is B438-9B76

 Directory of C:\Users\Pete\Documents\Dyalog APL-64 17.0 Unicode Files

23/06/2018  15:59    <DIR>          .
23/06/2018  15:59    <DIR>          ..
23/06/2018  14:53           181,488 default.dlf
13/06/2018  20:13         1,262,296 def_uk.dse
14/06/2018  14:36           108,976 UserCommand20.cache
               3 File(s)      1,552,760 bytes
               2 Dir(s)  101,371,097,088 bytes free

```

The system command [`)CMD`](../system-commands/cmd.md) provides a similar facility. A newer system function, [`⎕SHELL`](shell.md), can be used instead: it runs a program directly as well as through a shell, collects standard output and standard error separately, supplies input, sets the working directory and environment, imposes a timeout, and reports how the program ended rather than signalling an error.

## Right Argument

`Y` is either a simple character vector containing a command, which is [executed by the Command Processor](#executing-a-command), or a 2-element vector of character vectors, which [starts a program](#starting-a-program) directly.

## Result

Where `Y` is a command, `⎕CMD` waits for it to finish and `R` is a vector of character vectors, each element a line of the output it produced.

Where `Y` starts a program, `⎕CMD` returns immediately and the [shy](../../programming-reference-guide/introduction/results.md#shy-results) result `R` is an integer scalar holding the process identifier (PID).

## Executing a Command

The term command means an instruction recognised by the Command Processor, or the pathname of a program, with optional parameters, to be executed by it. `⎕CMD` invokes the Command Processor, normally `cmd.exe`, and passes the command to it.

If the command specified in `Y` already contains the redirection symbol (`>`) the capture of output through a pipe is avoided and the result `R` is empty.  If the command specified by `Y` issues prompts and expects user input, it is **ESSENTIAL** to explicitly redirect input and output to the console.

If this is done, APL detects the presence of a "`>`" in the command line, runs the command processor in a **visible** window, and does not direct output to the pipe.  If you fail to do this your system will appear to hang because there is no mechanism for you to receive or respond to the prompt.

<h3 class="example">Example</h3>

```apl
      ⎕CMD 'DATE <CON >CON'
```

(Command Prompt window appears)

`Current date is Wed 19-07-1995`

`Enter new date (dd-mm-yy): 20-07-95`

(COMMAND PROMPT window disappears)

### Spaces in Pathnames

If `Y` specifies a program (with or without parameters) and the pathname to the program  contains spaces, you must enclose the string in double-quotes.

For example, to start a version of Excel to which the pathname is:

```apl
   C:\Program Files\Microsoft Office\OFFICE11\excel.exe
```

the argument to `⎕CMD` should be:

```apl
⎕CMD '"c:\program files\microsoft office\office11\excel.exe"'

```

### Double-Quote Restriction

The Windows Command Processor does not permit more than one set of double-quotes in a command string.

The following statements are all valid:

```apl
⎕CMD 'c:\windows\system32\notepad.exe c:\myfile.txt'  
⎕CMD 'c:\windows\system32\notepad.exe "c:\myfile.txt"'
⎕CMD '"c:\windows\system32\notepad.exe" c:\myfile.txt'
```

Whereas the next statement, which contains two sets of double-quotes, will fail:

```apl
⎕CMD '"c:\windows\system32\notepad.exe" "c:\myfile.txt"'
```

Such a statement can however be executed using the second form of `⎕CMD`(where the argument is a 2-element vector of character vectors) which does not use the Windows Command Processor and is not subject to this restriction. However, the call to `⎕CMD` will return immediately, and no output from the command will be returned.

```apl
⎕CMD'"c:\windows\system32\notepad.exe" "c:\myfile.txt"' ''
```

### Implementation Notes

The right argument of `⎕CMD` is simply passed to the appropriate command processor for execution and its output is received using an *unnamed pipe*.

By default, `⎕CMD` will execute the string `('cmd.exe /c',Y)`; where `Y` is the argument given to `⎕CMD`.  However, the implementation permits the use of alternative command processors as follows:

Before execution, the argument is prefixed and postfixed with strings defined by the APL parameters CMD_PREFIX and CMD_POSTFIX.  The former specifies the name of your command processor and any parameters that it requires.  The latter specifies a string which may be required.  If CMD_PREFIX is not defined, it defaults to the name defined by the environment variable COMSPEC followed by  "/c".  If COMSPEC is not defined, it defaults to `cmd.exe`.  If CMD_POSTFIX is not defined, it defaults to an empty vector.

`⎕CMD` treats certain characters as having special meaning as follows:

|---|----------------------------------------------------------------------------|
|`#`|marks the start of a trailing comment,                                      |
|`;`|divides the command into sub-commands,                                      |
|`>`|if found within the last sub-command, causes `⎕CMD` to use a visible window.|

If you simply wish to open a Command Prompt window, you may execute the command as a Windows Program (see below).  For example:

```apl
      ⎕CMD 'cmd.exe' ''
```

## Starting a Program

Where `Y` is a 2-element vector of character vectors, `⎕CMD` starts the executable program named by `Y[1]` with the initial window parameter given by `Y[2]`, without going through the Command Processor.

`Y[1]` must specify the name or complete pathname of an executable program.  If the name alone is specified, Windows will search the following directories:

1. the current directory,
2. the Windows directory,
3. the Windows system directory,
4. the directories specified by the PATH variable,
5. the list of directories mapped in a network.

`Y[1]` can contain the complete command line, including any suitable parameters for starting the program.  If Windows fails to find the executable program, `⎕CMD` will fail and report `FILE ERROR 2`.
`Y[2]` must be one of the following, otherwise `⎕CMD` signals `DOMAIN ERROR`:

|`Y[2]`|Effect|
|---|---|
|`'Normal'`, `''`|Application is started in a normal window, which is given the input focus|
|`'Unfocused'`|Application is started in a normal window, which is not given the input focus|
|`'Hidden'`|Application is run in an invisible window|
|`'Minimized'`, `'Minimised'`|Application is started as an icon, which is not given the input focus|
|`'Maximized'`, `'Maximised'`|Application is started maximised (full screen) and is given the input focus|

There is no way to terminate an application started by `⎕CMD` from APL; it runs until it completes or is terminated by an external mechanism. Furthermore, if the window parameter is `'Hidden'`, the user is unaware of the application, unless it makes itself visible, and has no means to close it.

<h3 class="example">Examples</h3>

```apl
      Path←'c:\Program Files\Microsoft Office\Office\'
      ⎕←⎕CMD (Path,'excel.exe') ''
33
      ⎕CMD (Path,'winword /mMyMacro') 'Minimized'
```

## Which Form to Use

Either form of `⎕CMD` may be used to execute a program. The difference is that when the program is executed via the Command Processor, APL waits for it to complete and returns any result that the program would have displayed in the Command Window had it been executed from a Command Window. In the second case, APL starts the program (in parallel).

!!! Info "Information"
    This function is disabled and instead generates a `DOMAIN ERROR` if the RIDE_SPAWNED parameter is non-zero. This is designed to prevent it being invoked from a Ride session which does not support this type of user interface. For further details, see the [Ride User Guide](https://dyalog.github.io/ride).

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕CMD CMD
</div>
