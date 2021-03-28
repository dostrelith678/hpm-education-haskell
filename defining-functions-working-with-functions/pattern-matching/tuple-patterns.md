# Tuple Patterns

We can think of a tuple pattern as a tuple of lower-level patterns – the lower-level patterns match individual elements in the tuple. That tuple of patterns itself makes a full pattern that matches any tuple with the same length and whose elements match the internal patterns. We could use tuple patterns for functions that return the suit and the rank of a playing card represented by a tuple:

```haskell
getSuit :: (String, String) -> String
getSuit (suit, _) = suit

getRank :: (String, String) -> String
getRank (_, rank) = rank

ghci> getSuit ("Hearts", "Ace")
"Hearts"
ghci> getRank ("Hearts", "Ace")
"Ace"
```

We check that the tuple passed in is of length two, and then return the first or second element depending on what we want to get.

