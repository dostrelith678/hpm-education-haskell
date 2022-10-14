# Fold Left (foldl)

In `foldl`, the combining function (or operator) associates to the left, meaning the left-most elements will be evaluated first, i.e. the most nested parentheses will be on the left side of the data structure. Therefore, its definition using recursion on lists would be:

```haskell
foldl :: (a -> b -> a) -> a -> [b] -> a
foldl f v [] = v
foldl f v (x:xs) = foldl f (f v x) xs
```

So we take the second argument `v` and the head of the list `x` and apply the combining function on them, and then use that result to feed the recursive function for the rest of the list. The sum of a list using `foldl` would be applied like this:

```haskell
foldl (+) 0 [1, 2, 3]
foldl (+) (0 + 1) [2, 3]
foldl (+) ((0 + 1) + 2) [3]
foldl (+) (((0 + 1) + 2) + 3) []
((((0 + 1) + 2) + 3)
```

Notice that the places of the accumulator value `v` are switched in `foldl` relative to `foldr` in the combining function `f`. That is, in `foldr`, the first argument of the combining function is an element from the data structure, while in `foldl`, the first argument is the accumulator value and the second one is the element of the data structure. This may not be clear from the examples of `sum` and `product`, so let's implement a folding function that calculates the length of a list with both `foldr` and `foldl` using a lambda function as the combining function:

```haskell
lengthr :: [a] -> Int
lengthr = foldr (\_ n -> n + 1) 0  -- list element first, accumulator second
ghci> lengthr [1, 2, 3]
3
```

If we want to declare the same function with `foldl`, we have to reverse the arguments for the combining function to avoid a type error:

```haskell
lengthl :: [a] -> Int
lengthl = foldl (\n _ -> n + 1) 0  -- accumulator first, list element second
Prelude> lengthl [1, 2, 3]
3
```

