---
search:
  boost: 2
---

# <span>Division Behaviour</span> `⎕DIV`

`⎕DIV` determines what division by zero gives.

`⎕DIV` is an [implicit argument](../primitive-functions/notes.md#implicit-arguments) of:

- monadic functions: [`÷`](../primitive-functions/reciprocal.md)
- dyadic functions: [`÷`](../primitive-functions/divide.md)

<h2 class="example">Example</h2>

```apl
      1 0 2÷2 0 1
0.5 1 2
      ÷0 1
DOMAIN ERROR: Divide by zero
      ÷0 1
      ∧
      ⎕DIV←1
      ÷0 2
0 0.5
      1 0 2÷0 0 4
0 0 0.5
```

## Value

`⎕DIV` is one of:

- `0` – division by zero signals `DOMAIN ERROR`, except that `0÷0` is `1` (default).
- `1` – division by zero gives `0`, `0÷0` included.

Any other value signals `DOMAIN ERROR`. The configuration parameter [**DEFAULT_DIV**](../../windows-installation-and-configuration-guide/configuration-parameters/default-div.md) sets the value in a clear workspace.

## Scope

`⎕DIV` has [namespace scope](system-functions-by-category.md#system-variables). A new namespace starts with the value of the namespace that creates it, and a function that localises `⎕DIV` starts with its current value.

<!-- Hidden search keywords -->
<div style="display: none;">
  ⎕DIV DIV
</div>
