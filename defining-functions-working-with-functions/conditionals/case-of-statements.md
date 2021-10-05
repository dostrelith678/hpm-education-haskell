# Case-of Statements

There is another type of conditional statement called `case` which uses matching patterns to determine the expression to be evaluated. If you are familiar with switch statements from imperative programming, this is their equivalent in Haskell. The syntax is:

```haskell
case <EXPRESSION> of
  <PATTERN1> -> <EXPRESSION1>
  <PATTERN2> -> <EXPRESSION2>
  ...
  <PATTERNx> -> <EXPRESSIONx>
  _          -> <DEFAULT_EXPRESSION>
```

The `_` is a **wildcard character**. It is a useful tool for when we do not really care about whatever the value of the expression might be. In this case, whatever that value is – we know what we want to do if none of our previous cases match and assign it the default expression. For example, we could define a function that returns the colour of a playing card based on its suit:

```haskell
cardColour :: String -> String
cardColour suit =
  case suit of
    "hearts" -> "red"
    "diamonds" -> "red"
    "spades" -> "black"
    "clubs" -> "black"
    _ -> "I am not familiar with this card suit."
    
ghci> cardColour "diamonds"
"red"
ghci> cardColour "ace"
"I am not familiar with this card suit."
```

That is, for the four valid suits we return their respective colours. Anything else is covered by the wildcard case and no matter what the value is, we always choose the same course of action.

