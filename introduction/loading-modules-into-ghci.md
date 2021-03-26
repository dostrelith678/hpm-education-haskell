# Loading Modules into GHCi

Before we move on, let's see how we can load modules we create into GHCi, so that we can use any functions we define. We create a new file, e.g. `Practice.hs`, and define our module in there \(remember, the module name should match the file name\), and define our `triple` function from before:

```haskell
module Practice where

triple x = 3 * x
```

We can now launch GHCi from the terminal and load our module using its relative file path using `:load`, making the function available for use:

```bash
$ ghci
GHCi, version 8.10.2: https://www.haskell.org/ghc/ :? for help

{- Assuming our Practice.hs file is in the same directory from 
 which we launched GHCi -}

ghci> :load Practice.hs
[1 of 1] Compiling Practice ( Practice.hs, interpreted )
Ok, one module loaded.
*Practice> triple 3
9
```



