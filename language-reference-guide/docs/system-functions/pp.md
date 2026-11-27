---
search:
  boost: 2
---

# <span>Print Precision</span> `⎕PP`

`⎕PP` is the number of significant digits with which non-integer numbers are displayed.

`⎕PP` is an [implicit argument](../primitive-functions/notes.md#implicit-arguments) of:

- monadic functions: [`⍕`](../primitive-functions/format.md)
- system functions: [`⎕FMT`](format-monadic.md)
- other syntax: [`⎕`](evaluated-input-output.md) and [`⍞`](character-input-output.md) output

<h2 class="example">Example</h2>

```apl
      ÷3 6
0.3333333333 0.1666666667
      ⎕PP←3
      ÷3 6
0.333 0.167
```

## Value

`⎕PP` is an integer from `1` to `34`. Any other value signals `DOMAIN ERROR`. The configuration parameter [**DEFAULT_PP**](../../windows-installation-and-configuration-guide/configuration-parameters/default-pp.md) sets the value in a clear workspace, and its default is `10`.

`⎕PP` does not apply to integers, unless they are stored as floating-point numbers. That is the case for an integer in an array that also holds non-integers, and for an integer that is too large for an integer [data representation](dr.md). A floating-point number whose integer part has more digits than `⎕PP` is displayed in scaled form.

<h3 class="example">Example</h3>

```apl
      ⎕PP←3
      123456
123456
      123456 1234.5678
1.23E5 1.23E3
```

## Exact Conversion

If `⎕PP` is `17` or more when [`⎕FR`](fr.md) is `645`, or `34` when `⎕FR` is `1287`, a floating-point number can be converted to its character representation and back without losing precision. With exact comparison (`⎕CT` is `0`), `N=⍎⍕N` is then true for any floating-point number `N`.

## Exceptions

`⎕PP` does not apply in the following contexts:

- [Array notation output](../../programming-reference-guide/introduction/arrays/display-of-arrays.md#array-notation) (when `]APLAN.Output` is on)
- [`⎕JSON`](json.md) export
- [`⎕CSV`](csv.md) export

## Scope

`⎕PP` has [namespace scope](system-functions-by-category.md#system-variables). A new namespace starts with the value of the namespace that creates it, and a function that localises `⎕PP` starts with its current value.

## See Also

- [Display of Arrays](../../programming-reference-guide/introduction/arrays/display-of-arrays.md) – how arrays appear in the session

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕PP PP
</div>
