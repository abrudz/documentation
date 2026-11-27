---
search:
  boost: 2
---

# <span>Floating-Point Representation</span> `⎕FR`

`⎕FR` determines how floating-point numbers are represented, and therefore how floating-point arithmetic is done.

`⎕FR` is an [implicit argument](../primitive-functions/notes.md#implicit-arguments) of:

- monadic functions that compute real numbers: [`÷`](../primitive-functions/reciprocal.md), [`*`](../primitive-functions/exponential.md), [`⍟`](../primitive-functions/natural-logarithm.md), [`!`](../primitive-functions/factorial.md), [`○`](../primitive-functions/pi-times.md), [`⌹`](../primitive-functions/matrix-inverse.md)
- dyadic functions that compute real numbers: [`+`](../primitive-functions/plus.md), [`-`](../primitive-functions/minus.md), [`×`](../primitive-functions/times.md), [`÷`](../primitive-functions/divide.md), [`*`](../primitive-functions/power.md), [`⍟`](../primitive-functions/logarithm.md), [`|`](../primitive-functions/magnitude.md), [`!`](../primitive-functions/binomial.md), [`○`](../primitive-functions/circular-functions.md), [`∨`](../primitive-functions/greatest-common-divisor-or.md), [`∧`](../primitive-functions/lowest-common-multiple-and.md), [`⊥`](../primitive-functions/decode.md), [`⊤`](../primitive-functions/encode.md), [`⌹`](../primitive-functions/matrix-divide.md)
- monadic functions that perform tolerant comparisons: [`⌈`](../primitive-functions/ceiling.md), [`⌊`](../primitive-functions/floor.md), [`∪`](../primitive-functions/unique.md)
- dyadic functions that perform tolerant comparisons: [`~`](../primitive-functions/without.md), [`<`](../primitive-functions/less-than.md), [`≤`](../primitive-functions/less-than-or-equal-to.md), [`=`](../primitive-functions/equal-to.md), [`≥`](../primitive-functions/greater-than-or-equal-to.md), [`>`](../primitive-functions/greater-than.md), [`≠`](../primitive-functions/not-equal-to.md), [`≡`](../primitive-functions/match.md), [`≢`](../primitive-functions/not-match.md), [`⍳`](../primitive-functions/index-of.md), [`∊`](../primitive-functions/membership.md), [`∪`](../primitive-functions/union.md), [`∩`](../primitive-functions/intersection.md), [`⍷`](../primitive-functions/find.md)
- monadic functions that perform intolerant comparisons: [`⍒`](../primitive-functions/grade-down.md), [`⍋`](../primitive-functions/grade-up.md)
- dyadic functions that perform intolerant comparisons: [`⌈`](../primitive-functions/maximum.md), [`⌊`](../primitive-functions/minimum.md), [`⍒`](../primitive-functions/dyadic-grade-down.md), [`⍋`](../primitive-functions/dyadic-grade-up.md), [`⍸`](../primitive-functions/interval-index.md)
- operators: [`⌸`](../primitive-operators/key.md)
- system functions: [`⎕FX`](fx.md)

<h2 class="example">Example</h2>

```apl
      ⎕DR 0.1
645
      ⎕FR←1287
      ⎕DR 0.1
1287
```

## Value

`⎕FR` is one of:

- `645` – floating-point numbers are represented in the IEEE 754 [*binary64*](https://en.wikipedia.org/wiki/Double_precision_floating-point_format) format, with about 16 significant decimal digits and magnitudes up to about `1.8E308` (default).
- `1287` – floating-point numbers are represented in the IEEE 754-2008 [*decimal128*](https://en.wikipedia.org/wiki/Decimal128_floating-point_format) format, with 34 significant decimal digits and magnitudes up to about `1E6145`.

Any other value signals `DOMAIN ERROR`. The value in a clear workspace is `645`.

## Changing the Representation

Changing `⎕FR` affects only the floating-point numbers that are computed afterwards. Existing arrays keep their representation, so a workspace can hold numbers in both representations. A function that only rearranges an array, such as _take_ (`↑`), keeps its representation, while the result of a computation has the representation that `⎕FR` gives when it is computed, whatever the representation of its arguments:

```apl
      ⎕FR←1287
      x←1.1 2.2 3.3
      ⎕FR←645
      ⎕DR x
1287
      ⎕DR 2↑x
1287
      ⎕DR x+0
645
```

A decimal number whose magnitude is too large for the binary representation signals `DOMAIN ERROR` when it is used in a computation:

```apl
      ⎕FR←1287
      x←1E1000
      ⎕FR←645
      x+0
DOMAIN ERROR: ⎕FR=645 limits arithmetic to the range +/-1.79E308 (approx)
      x+0
       ∧
```

Comparisons use the tolerance for the current `⎕FR`, [`⎕CT`](ct.md) for `645` and [`⎕DCT`](dct.md) for `1287`. A decimal `1÷3` is equal to a binary one within `⎕CT`, but not within the much smaller `⎕DCT`:

```apl
      ⎕FR←1287
      x←1÷3
      ⎕FR←645
      x=1÷3
1
      x←1÷3
      ⎕FR←1287
      x=1÷3
0
```

## Constants

A numeric constant gets its representation from the value of `⎕FR` when the constant is read: for a Session line, before any of the line runs, and for a function, when the function is fixed. Changing `⎕FR` while an application runs is therefore not recommended.

<h3 class="example">Examples</h3>

The constant `0.1` is read before `⎕FR←1287` runs:

```apl
      ⎕FR←645
      ⎕FR←1287 ⋄ ⎕DR 0.1
645
      ⎕DR 0.1
1287
```

`Tenth` is fixed while `⎕FR` is `645`, so its constant stays binary:

```apl
      ⎕FR←645
      ∇ R←Tenth
        R←0.1
      ∇
      ⎕FR←1287
      ⎕DR Tenth
645
```

!!! Warning "Warning"
    Complex numbers are not recommended when `⎕FR` is `1287`:

    - Complex numbers are always binary, so inserting a complex number into a decimal array, or appending one to it, converts the whole array to binary complex numbers, which can lose precision.
    - Comparisons use `⎕DCT`, whose default of `1E¯28` is in effect `0` for complex numbers.

## Scope

`⎕FR` has [namespace scope](system-functions-by-category.md#system-variables). A new namespace starts with the value of the namespace that creates it, and a function that localises `⎕FR` starts with its current value.

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕FR FR
</div>
