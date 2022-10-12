# Introduction

A **higher-order function** in Haskell is a function that either takes in a function as its argument or returns a function as its result. We have already seen how functions can return other functions as their result when we introduced [curried functions](../types-in-haskell/function-types/curried-functions.md), so we will focus on **functions that take other functions as arguments** in this chapter. First, let's look at a simple example of a higher-order function that takes in a function and applies it twice to an argument:

```haskell
applyTwice :: (a -> a) -> a -> a
applyTwice f x = f (f x)

ghci> applyTwice (++ " two") "one"
"one two two"
```

The function we passed in `(++ "two ")` simply appends the string `"two "` to the argument passed in (in this case, it must be a string), and it is applied twice when the higher-order function `applyTwice` is called.

Now let's take a closer look at two higher-order functions that are defined in the Prelude for working with lists, `map` and `filter`.
