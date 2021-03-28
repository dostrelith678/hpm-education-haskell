# MultiWayIf

**MultiWayIf** allows us to create multiple cases for our if statements **without nesting** them. We define a sequence of expressions that evaluate to either `True` or `False` \(conditions called **guards**\) and associate an expression to each of them:

```haskell
if | <CONDITION1> -> <EXPRESSION1>
   | <CONDITION2> -> <EXPRESSION2>
   | ...
   | <CONDITIONx> -> <EXPRESSIONx>
   | otherwise -> <EXPRESSION>
```

The symbol `|` can be read as "such that..." or "where...". The guards are evaluated from top to bottom, and the expression associated with the first guard that is `True` is chosen for further evaluation. The `otherwise` function simply always evaluates to `True` and the expression associated with it will always be further evaluated if none of the guards before it evaluate to `True`. It gives us a convenient way to make sure that we have handled all possible cases. It is not necessary to add the `otherwise` guard at the end, but if all the possible cases are not met, we will end up with an error on runtime.

One more thing we have to do in order to use the `MultiWayIf` is to **enable the extension** in GHC. GHC has a number of special features like the `MultiWayIf` that are disabled by default so we have to add a line above our module declaration in the following format to enable it:

```haskell
{-# LANGUAGE MultiWayIf #-} 
module Practice where
...
```

Let's switch our `trackScore` function to use `MultiWayIf` instead, but not include the case where `time == avg`. It will result in an error at **runtime** \(not during compilation\), because the case we entered has not been defined:

```haskell
trackScore :: Float -> Float -> String
trackScore time avgTime = 
  if | time < avgTime -> "Great! Your time is " ++ show (avgTime - time) 
         ++ " seconds below average!"
     | time > avgTime -> "Your time is " ++ show (time - avgTime) ++ " 
         20seconds above average."

ghci> :r
[1 of 1] Compiling Practice ( practice.hs, interpreted )

*Practice> trackScore 10 10
"*** Exception: practice.hs:(74,1)-(76,89): Non-exhaustive patterns in 
function trackScore2
```

Let's fix it up:

```haskell
trackScore :: Float -> Float -> String
trackScore time avgTime = 
  if | time < avgTime -> "Great! Your time is " ++ show (avgTime - time) 
         ++ " seconds below average!"
     | time > avgTime -> "Your time is " ++ show (time - avgTime) ++ " 
         seconds above average."
     | otherwise -> "Your time is on par with the average time!"
```

This already reads much better than our first implementation with nested `if-statements`, but there is a way to make it even nicer by using **guarded equations**.

