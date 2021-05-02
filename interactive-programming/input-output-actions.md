# Input / Output Actions

Haskell uses a special type `IO` to distinguish impure, input/output actions from pure expressions. The idea of the `IO` type is that apart from returning some value, it may also interact with the outside world along the way. The `IO` type has the following structure:

```haskell
IO a
```

where `IO` is the type name, and a is the parameterised value that it returns. For example:

```haskell
IO Int -- an action that returns an Int
IO () -- an action that returns an empty tuple
```

The last example `IO ()` represents an action that is run solely for its side-effects and simply returns an empty tuple \(a void value\). Some **basic actions** in Haskell are:

```haskell
getChar :: IO Char -- reads and returns a character from the screen
putChar :: Char -> IO () -- prints a character to the screen
return :: a -> IO a -- returns a value as an action
```

Note that, strictly speaking, `putChar` and `return` are not actions, but functions that return actions. The `return` function is simply our one-way bridge from the pure world to the impure world that we use when we want to use our pure values in actions, which we will see in examples soon. For now, let's just try out the basic actions `getChar` and `putChar` in GHCi:

```haskell
ghci> getChar
1'1'            -- input is 1

ghci> getChar
'\n'


ghci> putChar 'a'
a

ghci> putChar '\n'

```



