# Ord – ordered types

The `Ord` class requires any type that wants to be an instance of it to first be an instance of the `Eq` class by using a **class constraint**, and additionally, to support the following methods:

```haskell
class (Eq a) => Ord a where
  (<), (<=), (>), (>=) :: a -> a -> Bool
  min, max :: a -> a -> a
```

In other words, the `Ord` class extends the `Eq` class and supports additional methods `(<)`, `(<=)`, `(>)`, `(>=)`, `min` and `max`. The `min` and `max` methods are defined by default as:

```haskell
min x y
 | x <= y = x
 | otherwise = y
 
max x y
 | x <= y = y
 | otherwise = x
```

And for a minimal definition of the class, we just need to define the `(<=)` method because the other ones also have default definitions:

```haskell
class (Eq a) => Ord a where
  (<), (<=), (>), (>=) :: a -> a -> Bool
  min, max :: a -> a -> a

    -- Minimal complete definition:
    -- (<=)
    
  x < y = x <= y && x /= y
  x > y = y < x
  x >= y = y <= x
  
  min x y
    | x <= y = x
    | otherwise = y
  max x y
   | x <= y = y
   | otherwise = x
```

All the basic types of Haskell are also instances of the `Ord` class.
