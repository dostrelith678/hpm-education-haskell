# Function Types

We know that **functions** in Haskell are **expressions** and each expression must have a type, so what types can a function have? Functions take in some arguments and create a result of some type which can be the same as some \(or all\) of its arguments or a different one. We have already touched upon the subject of function types in our example function `triple`:

```haskell
triple :: Int -> Int
triple x = 3 * x
```

In this case, the type of our function triple is `Int -> Int` – it takes an`Int`as its only argument and returns an`Int`as the result. As functions are expressions, we can use them as any other type of data, for example, we can create a list of functions:

```haskell
ghci> funList = [(+), (*)] -- (+) and (*) are functions for addition and multiplication
ghci> :t funList
Num a => [a -> a -> a]
```

We can see that `funList` is a list of a certain type – specifically, a **function type** that takes two arguments of type `Num` and returns a `Num` type as its result.

