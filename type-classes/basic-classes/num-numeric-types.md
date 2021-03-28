# Num – Numeric Types

The `Num` class supports basic numeric methods for its types:

```haskell
(+), (-), (*) :: a -> a -> a
negate, abs, signum :: a -> a
```

Notice that division is not included here because of how it is handled differently for integers floating-point numbers, as we will see in the next two classes \(`Integral` and `Fractional`\). The `signum` method returns the sign of a number \(-1 for negative numbers and 1 for positive ones\).

