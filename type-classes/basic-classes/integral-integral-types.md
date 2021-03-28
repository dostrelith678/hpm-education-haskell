# Integral – Integral Types

The `Integral` class extends the `Num` class and supports two additional methods for working with integral numbers, integer division and integer remainder:

```haskell
div, mod :: a -> a -> a

ghci> 5 `div` 3
1

ghci> 5 `mod` 3
2
```

Basic types `Int` and `Integer` are instances of the `Integral` class.

