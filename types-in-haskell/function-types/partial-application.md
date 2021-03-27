# Partial Application

**Curried functions** enable the usage of **partial application**, with which we can call a function with only some of its arguments and **get a function back as a result** for further usage. That way, we can create new functions from existing ones which can serve as a powerful tool. For example, with our `multiply` function, we can create a function that always multiplies a number by`2`:

```haskell
ghci> multiply2 = multiply 1 2

ghci> :t multiply2
multiply2 :: Num a => a -> a -- this function now takes only 1 argument

ghci> multiply2 5
10
```

