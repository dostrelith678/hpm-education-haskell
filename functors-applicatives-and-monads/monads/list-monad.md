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

The `return` method simply takes a value `x` and puts it into a `List` structure `[x]`. The `(>>=)` method for lists extracts all the values `x` from the list `m` and applies the function `f` to each of them, combining all the results in one final list. The bind operator, as with the [`Maybe` monad](maybe-monad.md), allows us to chain operations together with lists as well. With lists, these chaining operations will combine all output possibilities in a single result list.



