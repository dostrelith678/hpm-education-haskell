# Show – Showable Types

The `Show` class is used for types whose values can be represented as strings and support the `show` method. All the basic types of Haskell are also instances of the `Show` class.

```haskell
show :: a -> String

ghci> show False
"False"

ghci> show [1..3]
"[1, 2, 3]"
```

