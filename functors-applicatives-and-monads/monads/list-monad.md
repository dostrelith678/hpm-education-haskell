# List Monad

As we already mentioned in the [Applicatives](../applicative-functors.md#the-list-applicative) section, the underlying effect of `Lists` is support for _nondeterministic_ computations. `Maybe` computations can return either `Nothing` or a `Just` value, while `List` computations can return zero, one or multiple values based on their length. Let's see how this is defined in the `Monad` instance of `List`:

```haskell
instance Monad [] where
   -- return :: a -> [a]
   return x = [x]
   
   -- (>>=)  :: [a] -> (a -> [b]) -> [b]
   m >>= f  = [y | x <- m, y <- f x]
```

{% hint style="info" %}
The bind operator in this case is defined using [list comprehension](../../list-comprehensions/list-comprehensions.md). ****Can you define it using the functions [`map`](../../higher-order-functions/the-map-function.md) and [`concat`](http://zvon.org/other/haskell/Outputprelude/concat_f.html)?
{% endhint %}

The `return` method simply takes a value `x` and puts it into a `List` structure `[x]`. The `(>>=)` method for lists extracts all the values `x` from the list `m` and applies the function `f` to each of them, combining all the results in one final list. As with the [`Maybe` monad](maybe-monad.md), the bind operator,  allows us to chain operations together with lists as well. With lists, these chaining operations will combine all output possibilities in a single result list.

Let's take a look at a simple example of chaining list operations together. Imagine we want to model [mitosis](https://en.wikipedia.org/wiki/Mitosis), a process where a single cell divides into two identical daughter cells. First, we will create a function that will simply split a cell in two and call it mitosis:

```haskell
mitosis :: String -> [String] -- we will represent cells with simple strings
mitosis = replicate 2

ghci> ["Cell"] >>= mitosis
["Cell", "Cell"]
```

With the monadic instance of lists, we have a simple way of chaining multiple operations on lists. We can chain the result of multiple cell replications starting with one cell into one final list:

```text
ghci> ["Cell"] >>= mitosis >>= mitosis >>= mitosis
["Cell", "Cell", "Cell", "Cell", "Cell", "Cell", "Cell", "Cell"]
```

In this case, the `mitosis` function is applied to each element of the list, providing a resulting list to be passed to the subsequent functions.

The monadic instance of lists also allows us to use the [do notation](../../interactive-programming/sequencing-actions.md):

```haskell
threeGens :: String -> [String]
threeGens gen0 = do
        gen1 <- mitosis gen0
        gen2 <- mitosis gen1
        gen3 <- mitosis gen2
        return gen3
        
ghci> threeGens "Cell"
["Cell", "Cell", "Cell", "Cell", "Cell", "Cell", "Cell", "Cell"]
```

