# The Layout Rule

Before we dive into working with functions in Haskell, let's explore the **layout rule**. The layout rule states that each definition at the same level must begin at the same position in the script. This allows us to determine the groupings of different definitions simply from **indentation**. Let's define a function that adds together the squares of two numbers:

```haskell
sumSquares x y = a + b
  where
    a = x ^ 2 -- (^) is the power function
    b = y ^ 2
```

From the indentation, it is obvious \(both to us and Haskell\) that `a` and `b` are **local definitions** in the function `sumSquares`, defined using the `where`keyword. **Local definitions** exist as intermediate helper expressions that help us with structuring our functions and make our code more readable. It is also possible to wrap the local variables a and b in curly braces to explicitly state the grouping in which case the layout does not matter \(although it's best practice to use the layout rule to give our code better readability\), but we need to also explicitly separate each local definition with `;`:

```haskell
sumSquares x y = a + b
  where
    {
      a = x ^ 2; -- we need to separate expressions with ';' in this case
      b = y ^ 2
    }
```



