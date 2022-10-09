# Curried Functions

Functions in Haskell are also free to **return functions** as their results. This brings us to **curried functions** which take in **one argument at a time** and **return a function** that takes in additional arguments. Actually, all functions in Haskell with multiple arguments are applied this way (unless explicitly stated otherwise) – the function is first applied to the first argument and returns another function that is then applied to the second argument and so on. Let's explore this with an example \`multiply\` function that takes in three numbers and multiplies them:

```haskell
ghci> multiply x y z = x * y * z
ghci> :t multiply
multiply :: Num a => a -> a -> a -> a

-- a -> a -> a -> a actually means:
Num a => a -> (a -> (a -> a))
```

That is, `multiply` takes the argument `x` of type `a` and returns another function that takes in the argument `y` (also of type `a`) and returns another function that takes in the argument `z` (also of type `a`) that then returns the final result (also of type `a`). To avoid unnecessary parentheses, the function arrow `->` associates to the right by convention, while the function application associates to the left:

```haskell
multiply x y z
-- is actually:
((multiply x) y) z
```
