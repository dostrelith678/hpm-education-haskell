# Laziness

We are starting to define our own functions now, so it is a good time to explain the concept of laziness in Haskell. Haskell is a **lazy** programming language, which means it does not evaluate expressions until really necessary. The opposite of lazy evaluation is strict evaluation, in which all expressions in a function call are evaluated before they are passed to the function.

Let's take a look at an example to better understand this:

```haskell
ghci> f1 x y = x + 1
```

We see the function `f1` takes in two arguments, but completely ignores its second argument \`y\` during evaluation. Let's see what happens when we actually pass some arguments to the function:

```
ghci> f1 1 (2^58)
2
```

Of course, the final result is `2`, because `1 + 1 = 2`, but what happened with our second argument `(2 ^ 58)`? It was never needed during function execution so it was actually never evaluated. From this example, we can see how lazy evaluation can save computational time by not doing unnecessary computations.

However, there is also a drawback to this strategy - our second parameter was not completely ignored, but instead stored in memory as an unevaluated expression (2 ^ 58). These unevaluated expressions can build up in heap memory and cause memory leakage. That is, our programs can have increased memory usage for no useful reason and if they consume all our system memory, the program will crash.
