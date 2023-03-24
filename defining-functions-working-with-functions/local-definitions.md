# Local Definitions

We already saw how we can use `where` to define local helper expressions, but there is also another way. The `let`-`in` construct also allows us to define local expressions with the syntax `let <declarations> in <expression>`:

```haskell
sumSquares2 x y =
  let
    a = x ^ 2
    b = y ^ 2
  in
    a + b

ghci> sumSquares2 2 5
29
```

We can also use `let` -`in` and `where` in combination – for example, let's write a function that checks whether the sum of the squares of two numbers is a multiple of five:

```haskell
sumSquaresM5 x y =
  let
    sum = a + b
  in
    mod sum 5 == 0 -- (mod) is the modulo operator 
  where
    a = x ^ 2
    b = y ^ 2
```

We know a number is a multiple of five if the remainder of its division by five is zero. A thing to note is that there is a difference between `let`-`in` and `where`. What we define in `where` declarations is accessible to any code above it. However, the declarations from the `let` block are only accessible in the `in` block of the same `let-in` clause. For example, we could try to calculate the remainder from the division by five in the `where` clause using the `sum`from the `let` clause, but it will not work:

```haskell
sumSquaresM5 x y =
  let
    sum = a + b
  in
    res == 0
  where
    a = x ^ 2
    b = y ^ 2
    res = mod sum 5 -- the "sum" expression from let-in is not accessible here
```

The compilation of the above would result in an error as `sum` is only accessible in the `in` clause of the code. This means that with `let`-`in` we can create **super-localised expressions** that aren't accessible anywhere outside the `in` code block.
