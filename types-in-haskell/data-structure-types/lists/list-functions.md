# List Functions

Haskell comes with a number of useful functions for working with Lists in its`Data.List`module. This module is loaded by default in GHCi's Prelude:

```haskell
ghci> head [1, 2, 3] -- get the first element of a list
1

ghci> tail [1, 2, 3] -- exclude the first element from a list
[2, 3]

ghci> [1, 2] ++ [3, 4] -- join two lists together
[1, 2, 3, 4]

ghci> [1 .. 5] -- create a list of integers from 1 to 5
[1, 2, 3, 4, 5]

ghci> [1, 3 .. 10] -- list enumeration of integers with a step
[1, 3, 5, 7, 9]

ghci> [5, 4 .. 1] -- list enumeration of integers backwards
[5, 4, 3, 2, 1]

ghci> ['a' .. 'z'] -- enumeration even works with Chars
"abcdefghijklmnopqrstuvwxyz"

ghci> replicate 3 True -- create a list by replication
[True, True, True]

ghci> take 2 [1 .. 5] -- take the first 2 elements of a list
[1, 2]

ghci> drop 2 [1 .. 5] -- drop the first 2 elements of a list
[3, 4, 5]
```

As we mentioned before, everything in Haskell is immutable which means we cannot change an existing list, but we can create new ones from it. Lists are constructed from an empty list`[]`using an operator called cons`(:)`that constructs a list by adding new elements to the start of the list. For example, the list `[1, 2, 3, 4, 5]` is constructed in the following way:

```haskell
[1, 2, 3, 4, 5] => 1 : (2 : (3 : (4 : (5 : []))))
5 : []
4 : [5]
3 : [4, 5]
2 : [3, 4, 5]
1 : [2, 3, 4, 5]
[1, 2, 3, 4, 5]
```

