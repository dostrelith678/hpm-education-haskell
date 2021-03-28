# Read – readable types

The `Read` class supports reading and conversion of string representation of values into actual types using the `read` method. All the basic types of Haskell are also instances of the `Read` class. Note that we sometimes have to specify the type to be read in cases where the intended cannot be inferred:

```haskell
ghci> read "False"
*** Exception: Prelude.read: no parse

ghci> read "False" :: Bool
False
```

That is, in the first case, the compiler does not know whether to read `"False"` as a type of `String` or `Bool`, so it throws an exception, while in the second case, we explicitly state that we want to read it as a `Bool`. However, if we had some additional boolean function \(e.g. negation\) to be called on the read argument, the compiler could automatically infer the wanted type:

```haskell
ghci> not $ read "False"
True
```

