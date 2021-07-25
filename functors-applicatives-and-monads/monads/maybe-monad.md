# Maybe Monad

For our next example, let's imagine that we have a database that holds information about accounts and transactions - we don't have to worry about accessing the database right now, we just assume that a given account or transaction either exists in our database or doesn't. We could have the following type defined \(using type synonym declarations\):

```haskell
type Transaction = [Char] -- or String
type Account = [Char] -- or String
```

where both the `Transaction` and the `Account` instances are represented by strings \(e.g. through a hashing function\). Imagine that we now want to create a function that, given a `Transaction`, looks up both the `Account` from which the transaction originated and the destination `Account` in our database. There are three ways in which this function could fail:

1. The transaction is not found in our database
2. The origin account is not found in our database
3. The destination account is not found in our database

From what we already learned, we would write this function something like this:

```haskell
-- helper functions for finding transactions / accounts that may fail
findTransaction :: Transaction -> Maybe Transaction
findOriginAccount :: Transaction -> Maybe Account
findDestinationAccount :: Transaction -> Maybe Account

findAccounts :: Transaction -> Maybe (Account, Account)
findAccounts t =
    case findTransaction t of
        Nothing -> Nothing
        Just t ->
            case findOriginAccount t of
                Nothing -> Nothing
                Just originA ->
                    case findDestinationAccount t of
                        Nothing -> Nothing
                        Just destinationA ->
                            Just (originA, destinationA)
```

{% hint style="info" %}
Is it possible to write this function using [`Applicative`](../applicative-functors.md) form?
{% endhint %}

The important thing to notice here is the common pattern of exception checking at every step. At any point that we fail to find an element we are looking for, we want the function to handle this exception by returning `Nothing` , and we implement this very explicitly result in a long and hard-to-read function code. In other words, every step of the function depends on the result of the previous one \(or "binds" to the result of the previous one\). This is where we can take advantage of the fact that `Maybe` is a monad to simplify this by abstracting the error handling away.

First, let's look at the declaration of the `Monad`class in Haskell:

```haskell
class Applicative m => Monad m where
    return :: a -> m a
    (>>=)  :: m a -> (a -> m b) -> m b
    
    return = pure 
```

A `Monad` is therefore an `Applicative` that also supports the two methods,  `return` and `(>>=)` \(referred to as `bind`\). The `return` method wraps a value of any basic type `a` into the monad, returning a **monadic value**. The built-in declaration also has a default declaration for the `return` function, it is simply the `pure` method of the underlying `Applicative` that is used to wrap a value in the applicative constructor. The `(>>=)` takes a monadic value and a function that returns a monadic value and in general, applies that function to the first argument. Let's explore this in more detail with the implementation of the monad class for the `Maybe` type as an example :

```haskell
instance Monad Maybe where
    -- (>>=) :: Maybe a -> (a -> Maybe b) -> Maybe b
    Nothing >>= _ = Nothing
    (Just x) >>= f = f x
```

{% hint style="info" %}
Why don't we wrap the result of the function application `f x` into the `Maybe` type constructor `Just`?
{% endhint %}

For the `return` method, we keep the default declaration of `pure` which simply resolves to the `Just` constructor for the `Maybe` type. The `(>>=)` method exemplifies the main idea of monads, which is that we first look at the impure argument we receive \(in this case `Maybe a` \) and decide what to do from there. In that way, the function application depends on the result of the first argument \(or the underlying value of the first argument\). If `Maybe a` is a `Nothing` then we can completely ignore the function and simply propagate the exception with `Nothing`. Only if we know that the first argument is really a `Just a` do we unwrap the `a` value and apply the function `f` to it.

We can now re-write our `findAccounts` function in a simpler way using the fact that `Maybe` is a monad:

```haskell
findAccounts t =
  findTransaction t >>=
    (\tx -> findOriginAccount tx >>=
      (\origin -> findDestinationAccount tx >>=
        (\destination -> return (origin, destination) )))
```

That reads much better - we don't have to take care of every `Nothing` possibility as the monadic aspect of `Maybe` takes care of this for us. One thing to note that the `tx` argument is available at any step below the first "bind" all the lambda functions bind to one another in a sequence. The same applies to `origin` argument which we only use in the last step in order to `return` our result.

Does this kind of sequencing remind you of something we saw before? We used the `do` notation with [I/O actions](../../interactive-programming/sequencing-actions.md) to perform multiple actions in a sequence. As it turns out, the `do` notation is not specific to I/O actions but is actually just an alternative monad syntax and can be used with any monad. We can therefore re-write `findAccounts` using `do` notation:

```haskell
findAccounts t = 
  do
    tx          <- findTransaction t
    origin      <- findOriginAccount tx
    destination <-findDestinationAccount tx 
    return (origin, destination)
```

This now looks much more like an imperative language and we could say it actually is, with the imperative language it's written in being the `Maybe` language, which supports exceptions.`findTransaction`, `findOriginAccount` and `findDestinationAccount` are all statements in the imperative language of the `Maybe` monad. And this extends to all monads so that a value of type `M a` is interpreted as a statement  in an imperative language of `M` , with the semantics of that language being determined by the underlying monad `M` .

