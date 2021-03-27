# Static Type Check

We also said that Haskell is a statically-typed language, which means that each expression type is known at compile-time instead of run-time. This makes Haskell very reliable – if we successfully compile our program, we can be sure that no type errors will occur. This benefit does come at a cost of increased compilation time, and doing any changes to our program requires us to re-compile it.

Another feature of Haskell is type inference, which means that Haskell can automatically interpret types of expressions. This can make our code more concise, but it is still encouraged to explicitly specify the types when we define functions, i.e. to write the functions **type signature**. For our previous function triple, we could add a type signature to it in our `Practice.hs`:

```haskell
triple :: Int -> Int -- function type signature
triple x = 3 * x -- function definition
```

`triple :: Int -> Int` reads as "triple is a function that takes in one argument of the type `Int` and produces a result of a type `Int`". Now that we have altered our module code, we need to reload the practice module in order to apply the changes in GHCi:

```haskell
*Practice> :r Practice -- :r stands for :reload
Ok, one module loaded.

*Practice> :t triple -- :t stands for :type
triple :: Int -> Int

*Practice> triple 3
9
```

But what happens if we try to apply our `triple` function to a floating-point number?

```haskell
*Practice> triple 3.5
<interactive>:5:8: error:
 • No instance for (Fractional Int) arising from the literal ‘3.5’
 • In the first argument of ‘triple’, namely ‘3.5’
 In the expression: triple 3.5
 In an equation for ‘it’: it = triple 3.5
```

We get a type error because we strictly defined the function as one that takes in an Int as its only argument, but we passed in a floating-point number. So how can we make our function accept both `Int`and `Float`? To do that, we can use Haskell's polymorphism and specify a polymorphic type of `Num` \(an **overloaded type** specified with a **type class** - more on those later on\), which supports both integer and floating-point numbers:

```haskell
triple :: Num a => a -> a
triple x = 3 * x
*Practice> :r
*Practice> triple 3.5
10.5
```

The line `triple :: Num a => a -> a` now reads as "triple is a function that takes in one argument of type `a` and gives a result of type `a` where the type of `a` is `Num`". So here we see an example of **polymorphism** where we can work with different types for the same function argument. Note that we use the variable named `a` as a placeholder for the **type** **class** `Num`, but it could be any valid name starting with a lowercase character.

