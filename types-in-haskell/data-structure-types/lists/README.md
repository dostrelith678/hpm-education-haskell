# Lists

## Lists

**Lists** are sequences of elements of the **same type** and are a key component of Haskell. This means that a list can only hold elements of the same type, e.g. a list of `Ints` as we used in our example function - `sum`. To create lists in Haskell, we put their elements in square brackets and separate them with commas:

```haskell
[False, False, True] :: [Bool] -- a list of booleans
[1, 3, 5] :: [Int] -- a list of integers
['a', 'b', 'c'] :: [Char] -- a list of characters
```

Lists can also contain other lists:

```haskell
[[1, 2, 3], [4, 5, 6]] :: [[Int]] -- a list of lists of integers
```

But remember - lists are sequences of elements of the same type, so a list of lists must not contain lists of different types. For example, we cannot combine a list of `Ints` and a list of `Chars` into a single list of lists:

```haskell
ghci> x = [[1, 2, 3], ['a', 'b', 'c']]

<interactive>:2:7: error:
    • No instance for (Num Char) arising from the literal ‘1’
    • In the expression: 1
      In the expression: [1, 2, 3]
      In the expression: [[1, 2, 3], ['a', 'b', 'c']]
```

Lists can also be empty \(`[]`\) and a special case called a **singleton** list is \(`[[]]`\), which is a list with its single element being an empty list.

