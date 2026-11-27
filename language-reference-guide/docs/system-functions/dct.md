---
search:
  boost: 2
---

# <span>Decimal Comparison Tolerance</span> `⎕DCT`

`⎕DCT` is the relative tolerance within which two numbers are judged to be equal when [`⎕FR`](fr.md) is `1287`, in the [same way](ct.md#tolerant-equality) that [`⎕CT`](ct.md) is when `⎕FR` is `645`.

`⎕DCT` is an [implicit argument](../primitive-functions/notes.md#implicit-arguments) of:

- monadic functions: [`⌈`](../primitive-functions/ceiling.md), [`⌊`](../primitive-functions/floor.md), [`∪`](../primitive-functions/unique.md), [`≠`](../primitive-functions/unique-mask.md)
- dyadic functions: [`~`](../primitive-functions/without.md), [`<`](../primitive-functions/less-than.md), [`≤`](../primitive-functions/less-than-or-equal-to.md), [`=`](../primitive-functions/equal-to.md), [`≥`](../primitive-functions/greater-than-or-equal-to.md), [`>`](../primitive-functions/greater-than.md), [`≠`](../primitive-functions/not-equal-to.md), [`≡`](../primitive-functions/match.md), [`≢`](../primitive-functions/not-match.md), [`⍳`](../primitive-functions/index-of.md), [`∊`](../primitive-functions/membership.md), [`∪`](../primitive-functions/union.md), [`∩`](../primitive-functions/intersection.md), [`⍷`](../primitive-functions/find.md), [`|`](../primitive-functions/magnitude.md), [`∨`](../primitive-functions/greatest-common-divisor-or.md), [`∧`](../primitive-functions/lowest-common-multiple-and.md)
- operators: [`⌸`](../primitive-operators/key.md)
- system functions: [`⎕FMT`](format-dyadic.md)

<h2 class="example">Example</h2>

The constants are decimal numbers, because `⎕FR` is `1287` when the line that contains them is entered:

```apl
      ⎕FR←1287
      ⎕DCT←1E¯10
      1.00000000001 1.0000001 = 1
1 0
```

## Value

`⎕DCT` is a number from `0` to `2*¯32` (about `2.3E¯10`), and `0` makes comparisons exact. Any other value signals `DOMAIN ERROR`. The value in a clear workspace is `1E¯28`.

## Scope

`⎕DCT` has [namespace scope](system-functions-by-category.md#system-variables). A new namespace starts with the value of the namespace that creates it, and a function that localises `⎕DCT` starts with its current value.

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕DCT DCT
</div>
