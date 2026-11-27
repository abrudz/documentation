---
search:
  boost: 2
---

# <span>Comparison Tolerance</span> `⎕CT`

`⎕CT` is the relative tolerance within which two floating-point numbers are judged to be equal.

`⎕CT` is an [implicit argument](../primitive-functions/notes.md#implicit-arguments) of:

- monadic functions: [`⌈`](../primitive-functions/ceiling.md), [`⌊`](../primitive-functions/floor.md), [`∪`](../primitive-functions/unique.md), [`≠`](../primitive-functions/unique-mask.md)
- dyadic functions: [`~`](../primitive-functions/without.md), [`<`](../primitive-functions/less-than.md), [`≤`](../primitive-functions/less-than-or-equal-to.md), [`=`](../primitive-functions/equal-to.md), [`≥`](../primitive-functions/greater-than-or-equal-to.md), [`>`](../primitive-functions/greater-than.md), [`≠`](../primitive-functions/not-equal-to.md), [`≡`](../primitive-functions/match.md), [`≢`](../primitive-functions/not-match.md), [`⍳`](../primitive-functions/index-of.md), [`∊`](../primitive-functions/membership.md), [`∪`](../primitive-functions/union.md), [`∩`](../primitive-functions/intersection.md), [`⍷`](../primitive-functions/find.md), [`|`](../primitive-functions/magnitude.md), [`∨`](../primitive-functions/greatest-common-divisor-or.md), [`∧`](../primitive-functions/lowest-common-multiple-and.md)
- operators: [`⌸`](../primitive-operators/key.md)
- system functions: [`⎕FMT`](format-dyadic.md)

<h2 class="example">Example</h2>

`0.1+0.2` is not exactly `0.3` as a binary floating-point number, but it is within the tolerance:

```apl
      0.3=0.1+0.2
1
      ⎕CT←0
      0.3=0.1+0.2
0
```

## Tolerant Equality

Two numbers `X` and `Y` are judged to be equal if `(|X-Y)≤⎕CT×(|X)⌈|Y`, where `≤` is applied without tolerance. The tolerance is therefore relative to the larger magnitude of the two numbers, and a number is only equal to `0` if it is exactly `0`.

If [`⎕FR`](fr.md) is `1287`, the tolerance is [`⎕DCT`](dct.md) instead.

<h3 class="example">Example</h3>

```apl
      ⎕CT←1E¯10
      1.00000000001 1.0000001 = 1
1 0
```

## Value

`⎕CT` is a number from `0` to `2*¯32` (about `2.3E¯10`), and `0` makes comparisons exact. Any other value signals `DOMAIN ERROR`. The value in a clear workspace is `1E¯14`.

## Scope

`⎕CT` has [namespace scope](system-functions-by-category.md#system-variables). A new namespace starts with the value of the namespace that creates it, and a function that localises `⎕CT` starts with its current value.

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕CT CT
</div>
