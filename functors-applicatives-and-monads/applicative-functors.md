# Applicative Functors

The missing functionality of functors is obvious - `fmap` only works for functions that take in exactly 1 argument and applies that function to each individual element of a given data structure. But we might want to apply a function that takes multiple arguments - for example, how can we add together two values of the `Maybe` type? We could write our own function specific to that need:

```haskell
maybeAdd :: Maybe Int -> Maybe Int -> Maybe Int
maybeAdd (Just x) (Just y) = Just (x + y)
maybeAdd _ _ = Nothing

ghci> maybeAdd (Just 5) (Just 3)
Just 8
```

But that way we would have to write a new custom-made function for every function we would like to apply to two \(or more\) `Maybe` types - for example, multiplication.

This is where **Applicative Functors** _****_\(or **Applicatives**\) come into play. Applicatives generalise applying pure functions to **effectful** arguments \(such as the `Maybe` type\) instead of plain values. The effect of the `Maybe` type is the possibility of failure, and we will explore the effects of some other data types later.  The definition of `Applicative` is:

```haskell
class (Functor f) => Applicative f where
    pure  :: a -> f a
    (<*>) :: f (a -> b) -> f a -> f b
```

Firstly, for a type to become an instance of `Applicative` , it must be an instance of the `Functor` class. The `pure` method is used to transform arbitrary values into the functor data structure `f a`. The `(<*>)` method is very similar to that of `fmap` , but in this case, the function being applied is itself wrapped into the functor data structure `f (a -> b)` - this is exactly what allows us to use currying and apply functions that take an unlimited number of arguments on `Applicative` data instances.

### The Maybe Applicative

Let's look at how the `Maybe` type is made an instance of the `Applicative` class in the `Prelude` :

```haskell
instance Applicative Maybe where
    pure                  = Just
    (Just f) <*> (Just x) = Just (f x)
    _        <*> _        = Nothing
```

`pure` wraps a value with the `Just` constructor, and `(<*>)` applies the function to the value if neither of the arguments has failed, otherwise, it results in `Nothing`. Now we can simply calculate the sum of two `Maybe` types without the need for defining a function:

```haskell
ghci> pure (+) <*> Just 5 <*> Just 3
Just 8
```

We first use `pure` on the addition function `(+)` in order to wrap it into a `Maybe` and then apply it to the two arguments. Let's take a closer look at how the application is executed and keep track of types:

```haskell
-- pure transforms the (+) into an instance of an Applicative
ghci> :t pure (+)
pure (+) :: (Applicative f, Num a) => f (a -> a -> a)

ghci> :t pure (+) <*> Just 5
pure (+) <*> Just 5 :: Num a => Maybe (a -> a)
-- <*> applies the (+) function (wrapped into a Maybe) to the first argument
-- it returns a curried function wrapped in the Maybe constructor

ghci> :t pure (+) <*> Just 5 <*> Just 3
pure (+) <*> Just 5 <*> Just 3 :: Num b => Maybe b
-- finally, the curried function is applied to the second argument
-- and the addition is complete and results in a Maybe b
```

The final result is of the type `Maybe b` so the underlying **effect** of the `Maybe` type - the possibility of failure - is handled by the applicative style of function application. In other words, we do not have to define any additional functions to handle specific `Nothing` cases, as they are already defined in the `Applicative` instance definition for `Maybe`:

```haskell
ghci> pure (+) <*> Just 5 <*> Nothing
Nothing

ghci> pure (+) <*> Nothing <*> Just 3
Nothing
```

### The List Applicative

The `List` applicative is implemented in a way that function application through `(<*>)` applies the function in every possible combination of the arguments \(as a Cartesian product in mathematics\). So the underlying **effect** of the `List`  type is the possibility of results. The `Applicative` instance declaration for `List` is:

```haskell
instance Applicative [] where
    pure x = [x]
    fs <*> xs = [f x | f <- fs, x <- xs]
```

With that, we can apply functions on `List` types through `(<*>)`:

```haskell
ghci> pure (+) <*> [1,2] <*> [3,4]
[4,5,5,6]
-- 1 + 3
-- 1 + 4
-- 2 + 3
-- 2 + 4

ghci> [(+10), (*10), (^2)] <*> [1,2,3]
[11,12,13,10,20,30,1,4,9]
```

In the second example, each of the functions in the first list is a curried function that takes in one additional argument, and the result of the applicative action is applying all the functions from the first list to all the arguments of the second list.

{% hint style="info" %}
For those curious, there is also an implementation that matches only one argument per function - ZipList \([http://hackage.haskell.org/package/base-4.11.1.0/docs/Control-Applicative.html\#t:ZipList](http://hackage.haskell.org/package/base-4.11.1.0/docs/Control-Applicative.html#t:ZipList)\)
{% endhint %}

### The IO Applicative

The `IO` type refers to the impure world of Haskell, and its underlying **effect** _****_is the ability to perform input/output actions. Therefore, the applicative instance of the `IO` type supports the application of pure functions to impure arguments, and can also handle sequencing and extraction of result values:

```haskell
instance Applicative IO where
    pure = return
    a <*> b = do
        f <- a
        x <- b
        return (f x)
```

`pure` is simply our `return` function that wraps a pure value into an `IO` type, and given two impure arguments \(`IO` actions\), `(<*>)` performs the action `a` to get the function `f` and the action `b` to get the argument `x` , and finally returns `f x` - the result of that function application to the argument wrapped in the `IO` type.

As was mentioned before, the use of applicative style can handle both **sequencing** and **extraction** of values, so to define a function that reads two characters and returns their concatenation, instead of:

```haskell
read2 :: IO String
read2 = do
    a <- getLine
    b <- getLine
    return (a ++ b)
```

we can simply write:

```haskell
read2 :: IO String
read2 = pure (++) <*> getLine <*> getLine

ghci> read2
Applicative
Functors
"ApplicativeFunctors"
```

Furthermore, it becomes much easier to create a function that reads an arbitrary `n` number of lines and concatenates them with applicative style and recursion:

```haskell
getLines :: Int -> IO String
getLines 0 = return []
getLines n = pure (++) <*> getLine <*> getLines (n - 1)

ghci> getLines 5
1
2
3
4
5
"12345"
```

### Applicative Laws

There are four laws applicative functors must follow:

```haskell
pure id <*> v = v                            -- Identity
pure f <*> pure x = pure (f x)               -- Homomorphism
u <*> pure y = pure ($ y) <*> u              -- Interchange
pure (.) <*> u <*> v <*> w = u <*> (v <*> w) -- Composition
```

The `Identity` law states that applying the `id` function to an argument in applicative style returns the unaltered argument, much like we saw in functors.

The `Homomorphism` law states that `pure` preserves function application in the sense that applying a pure function to a pure value is the same as calling `pure` on the result of normal _function application_ to that value \(`f x`\).

The `Interchange` law states that the order in which we evaluate components doesn't matter in the case when we apply an effectful function to a pure argument. The `($ y)` is used to supply the argument `y` to the function `u`. A simpler example of using `($ y)`:

```haskell
ghci> map ($ 2) [(2*), (4*), (8*)]
[4,8,16]
```

The `Composition` law states that _function composition_ `(.)` __works with the `pure` function as well, so that `pure (.)` composes functions, i.e. composing functions `u` and `v` with `pure (.)` and applying the composed function to `w` gives the same result as to simply applying both functions `u` and `v` to the argument `w`.

