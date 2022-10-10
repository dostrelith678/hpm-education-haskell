# Function Operators

Sometimes our code can become difficult to read when using a large number of parentheses. This usually happens when we want to apply multiple functions to the same arguments and we use parentheses to determine how we want to apply those functions. For example, imagine a simple function that determines whether the square of an integer is greater than 100 with the use of helper functions `square` and `gt100`:

```haskell
square :: Int -> Int
square x = x * x

gt100 :: Int -> Bool
gt100 x = x > 100

squareGt100 :: Int -> Bool
squareGt100 x = gt100 (square x)
```

Because we are applying both `gt100` and `square` functions to the same argument, we can compose them into one and avoid parentheses altogether by applying that composed function to the argument. This is achieved through two function operators, **function composition** and **function application** operators:

1\) The function composition operator is `(.)`, and it is simply another function that returns a composed function as its result. This is how it is defined in the Prelude:

```haskell
(.) f g = \x -> f (g x)
```

It takes in two functions and returns a nameless lambda function that applies both functions to an argument, so it composes two functions into one. Note that the **function composition associates to the right**, i.e. the function on the right will be applied first, and then the function on the left will be applied to the result.

2\) The function application operator is `($)`, and it simply applies the given function to the given argument. This is how it is defined in the Prelude:

```haskell
f $ x = f x
```

We can use function composition in the definition of the `squareGt100` function:

```haskell
squareGt100 :: Int -> Bool
squareGt100 x = gt100 . square $ x
```

That is, we first compose the two functions, `gt100` and `square` and then apply the composed function to the argument `x`. Note that we could also use just the function composition operator, but in that case, we would still have to use parentheses:

```haskell
squareGt100 :: Int -> Bool
squareGt100 x = (gt100 . square) x

ghci> squareGt100 9
False
ghci> squareGt100 11
True
```
