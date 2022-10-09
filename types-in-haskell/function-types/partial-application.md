# Partial Application

**Curried functions** enable **partial application**, which can be used to call a function with only some of its arguments and **get a function back as a result** for further use. That way, we can create new functions from existing ones which can serve as a powerful tool. For example, with our `multiply` function, we can create a function that always multiplies a number by`2`:

```haskell
ghci> multiplyBy2 = multiply 1 2

ghci> :t multiplyBy2
multiply2 :: Num a => a -> a -- this function takes only 1 argument

ghci> multiplyBy2 5
10
```
