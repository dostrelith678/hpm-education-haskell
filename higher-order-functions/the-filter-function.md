# The filter Function

The `filter` function is another higher-order function for working with lists. As the name suggests, it is used for filtering lists by selecting **only elements that satisfy a predicate** defined by the function passed in. Like `map`, we could also define filter using a list comprehension:

```haskell
filter :: (a -> Bool) -> [a] -> [a]
filter f xs = [x | x <- xs, f x]
```

Unlike `map`, the `filter` function must receive a function that returns a boolean as its argument, and the resulting list from `filter` will always be of the same type as the list we passed in as we are only selecting elements from that list, rather than applying the function on them. We can `filter` a list using our `squareGt100` function from before in order to get the elements for which `squareGt100` returns `True`:

```haskell
ghci> filter squareGt100 [7..12]
[11,12]
```

Here are some other examples of using `filter` with other pre-defined functions:

```haskell
ghci> filter odd [1..5] -- get all odd numbers from a list
[1,3,5]

ghci> filter (\x -> length x > 2) ["a", "abc"] -- length greater than 2
["abc"]

ghci> filter (\(x:xs) -> x == 'a') ["cardano", "ada"] -- staring with 'a'
["ada"]
```



