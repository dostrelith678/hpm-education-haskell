# Data Declarations

With the keyword `Data`, we can define new types rather than just synonyms for already existing ones. For example, we can create a type that represents a card suit:

```haskell
data Suit = Hearts
          | Diamonds
          | Spades
          | Clubs
```

`Suit` is the **type name** in this definition, and the values \(`Hearts`, `Diamonds`, `Spades` or `Clubs`\) are **data constructors**. It states that the new type `Suit` can have **one of the four values** \(the `|` symbol stands for "or"\). This means `Suit` is a sum-type, which is any type that has multiple possible representations. Another example of a sum-type would be `Bool` which can be either `True` or `False`. 

Both the type name and its constructors must begin with a capital letter, and **constructors must be unique** to that type, i.e. the same constructor cannot be defined in more than one type. Once a new type is defined, it can be used in functions just like any other data type in Haskell. Just to illustrate, a very simple function to get the card suit in a string format would be:

```haskell
suitStr :: Suit -> String
suitStr Hearts = "... of hearts."
suitStr Diamonds = "... of diamonds."
suitStr Spades = "... of spades."
suitStr Clubs = "... of clubs."

ghci> suitStr Hearts
"... of hearts."
```



