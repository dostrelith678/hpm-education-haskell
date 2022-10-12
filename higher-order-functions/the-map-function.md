# The map Function

The `map` function takes in a function and a list, and applies the given function to each element of that list. As we have seen how list comprehensions work in the previous chapter, we could define `map` as:

```haskell
map :: (a -> b) -> [a] -> [b]
map f xs = [f x | x <- xs]
```

Note that the type variables `a` and `b` in the function definition could represent the same type, but this definition gives us flexibility so that a function passed in that takes in one type (`a`) can return another type (`b`), in which case we end up with a list of the type `[b]`. For example, we can pass our function `squareGt100` to a list of numbers and end up with a list of booleans:

```haskell
ghci> map squareGt100 [7..12]
[False, False, False, False, True, True]
```

Here are some other examples of using `map` with other pre-defined functions:

```haskell
ghci> map (* 2) [1..5] -- multiply each number in the list by 2
[2, 4, 6, 8, 10]

ghci> map not [True, False] -- not function reverses the boolean value
[False, True]

ghci> map reverse ["Cardano", "ADA"] -- reverse a given list (strings are lists of chars)
["onadraC","ADA"]

ghci> map ("Hi, " ++) ["Joe", "Jan"]
["Hi, Joe","Hi, Jan"]
```

