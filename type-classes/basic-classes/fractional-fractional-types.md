# Fractional – Fractional Types

The `Integral` class extends the `Num` class and supports two additional methods for working with floating-point numbers, fractional division and reciprocation:

```haskell
(/) :: a -> a -> a
recip :: a -> a

ghci> 5.0 / 2.0
2.5

ghci> recip 10 -- reciprocal is simply 1 / x
0.1
```

