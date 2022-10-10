# Lambda functions

**Lambda functions** are anonymous (or nameless) functions. This means that they can be applied without having an explicit declaration, i.e. the **function declaration and application are merged into one**. Similar to normal functions, the syntax for lambda functions includes its arguments and a function body that specifies how the result is calculated. However, instead of using a name for the function, we use the backslash symbol `"\"` (similar to the Greek letter lambda – λ), and instead of the equality symbol, we use the function arrow `"->"`:

```haskell
\<ARGUMENT1> <ARGUMENT2> -> <FUNCTION BODY>
```

We can directly use lambda functions just like any other function, so here is how we could use our `triple` function as a lambda function:

```haskell
ghci> (\x -> x * 3) 4
12
```

Lambda functions are very useful for functions that are only used locally because we can simplify our code. For example, our previously defined function `trackScore` could be improved by using a lambda function to calculate the score:

```haskell
trackScore4 :: Float -> Float -> String
trackScore4 time avgTime
  | time < avgTime = "Great! Your time is " ++ show (score) ++ " 
      seconds below average!"
  | time > avgTime = "Your time is " ++ show (score) ++ " seconds 
      above average."
  | otherwise = "Your time is on par with the average time!"
    where
      score = (\x y -> abs (x - y)) time avgTime
```

