# Enum – Enumeration Types

The last class we will look at here is the `Enum` class which supports operations on sequentially ordered types. We have already used this class in `[1..3]` for creating a list of elements from `1` to `3`.

```haskell
class Enum a where
  succ, pred :: a -> a
  toEnum :: Int -> a
  fromEnum :: a -> Int
  enumFrom :: a -> [a] -- [n..]
  enumFromThen :: a -> a -> [a] -- [n, n'..]
  enumFromTo :: a -> a -> [a] -- [n..m]
  enumFromThenTo :: a -> a -> a -> [a] -- [n, n'..m]
```

We do not have to worry about the implementation details of the Enum class at this point, but we can see that with an `Enum` class, we have access to the `[..]` methods which can be very useful.

