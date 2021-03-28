# Pattern Matching

**Pattern matching** is similar to conditional statements and allows us to chose different paths for our functions based on patterns of their arguments. These patterns can be direct values or more general patterns of arguments that the function takes in. Much like in guarded equations, the patterns are evaluated from top to bottom and the first one that matches the input arguments is selected for further evaluation. We can define our previous function `cardColour` using pattern matching with direct values:

```haskell
cardColour :: String -> String
cardColour "hearts" = "red"
cardColour "diamonds" = "red"
cardColour "spades" = "black"
cardColour "clubs" = "black"
cardColour _ = "I am not familiar with this card suit."

ghci> cardColour "diamonds"
"red"
ghci> cardColour "ace"
"I am not familiar with this card suit."
```

That is, we define multiple patterns for our function to account for different card suits and the wildcard character performs the same as we saw before in conditional statements. Pattern matching gets more powerful when we use it with lists and tuples to build larger patterns.

