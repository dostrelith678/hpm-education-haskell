# Guarded Equations

**Guarded equations** provide an alternative to if-else statements and are especially useful when we need multiple ifs in our code. Like `MultiWayIfs`, they represent a sequence of expressions that evaluate to either True or False \(conditions\) which are individually called guards and are used to decide the flow of the program. The syntax is very similar to `MultiWayIf` syntax and allows us to get rid of the `if` altogether:

```haskell
trackScore :: Float -> Float -> String
trackScore time avgTime
  | time < avgTime = "Great! Your time is " ++ show (avgTime - time) ++ "
      seconds below average!"
  | time > avgTime = "Your time is " ++ show (time - avgTime) ++ " 
      seconds above average."
  | otherwise = "Your time is on par with the average time!"
```

Note that in the above implementation of **guarded equations**, we have **moved the equation sign** in the line `trackScore time avgTime`, and we have **replaced the ifs arrow** `(->)` with it.

