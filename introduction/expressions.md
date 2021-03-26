# Expressions

We said applying functions to arguments is the basic method of computation in Haskell – the building blocks of Haskell programs. In that sense, expressions in Haskell would be what those building blocks are made of. Expressions can represent some primitive values, e.g. numbers, characters, or booleans \(`True`/ `False`\), and in that case, they are **irreducible** expressions, meaning they cannot be further simplified. On the other hand, there are **reducible** expressions, which can be evaluated to their final irreducible form.

Let's use GHCi to explore some Haskell expressions \(`ghci>` denotes code that is evaluated in GHCi\):

```text
ghci> 2 + 2 -- reducible expression
4
ghci> 10 -- irreducible expression
10
```

Notice that any reducible expression is actually a function applied to some arguments \(in this case the addition operator `(+)`. So any function in Haskell is at its core – an expression.

