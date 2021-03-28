# Exercise – Making a Card Deck Type

Let's now try to implement a data type that will represent a deck of cards. First, we can think about what type would be fitting for a card deck – a list of cards would be a good representation. But then what type is fitting for a single card? **Each card should have a rank and a suit** so we can make another type for cards that has the type of a tuple `(Rank, Suit)`. Let's start at the lowest level, the `Rank` and `Suit` type, and remember that we already defined the `Suit` type, but we will now also derive the `Show` class for it:

```haskell
data Suit = Hearts
  | Diamonds
  | Spades
  | Clubs
    deriving (Show)
```

which leaves us with the task of defining `Rank` for which we can also use nullary constructors and also derive some built-in classes:

```haskell
data Rank = Deuce
  | Three
  | Four
  | Five
  | Six
  | Seven
  | Nine
  | Ten
  | Jack
  | Queen
  | King
  | Ace
    deriving (Show, Eq, Ord, Enum)
```

We can then already use methods of those classes on the `Rank` type:

```haskell
ghci> Deuce < Three
True

ghci> Deuce <= Three
True

ghci> Deuce == Three
False

ghci> Deuce > Three
False

ghci> [Deuce .. Five]
[Deuce, Three, Four, Five]
```

We have the `Rank` and `Suit` types now, and we can simply define the type of Card as a type synonym for a tuple of `(Rank, Suit)`:

```haskell
type Card = (Rank, Suit)
```

Similarly, we can define a deck of cards as a type synonym for a list of `Card` types:

```haskell
type Deck = [Card]
```

We have all the required types for actually building a deck now, so let's make a function for that purpose. We will use list comprehension and take advantage of the fact that `Rank` supports enumeration:

```haskell
buildDeck :: Deck
buildDeck = [(rank, suit) | rank <- [Deuce .. Ace], suit <- suitList]
  where
    suitList = [Hearts, Diamonds, Spades, Clubs]
```

And we can now build a deck of cards using that function:

```haskell
ghci> deck = buildDeck
ghci> show deck
"[(Deuce, Hearts),(Deuce, Diamonds),(Deuce, Spades),(Deuce, Clubs),
(Three, Hearts),(Three, Diamonds),(Three, Spades),(Three, Clubs),(Four, 
Hearts),(Four, Diamonds),(Four, Spades),(Four, Clubs),(Five, Hearts),
(Five, Diamonds),(Five, Spades),(Five, Clubs),(Six, Hearts),(Six, 
Diamonds),(Six, Spades),(Six, Clubs),(Seven, Hearts),(Seven, Diamonds),
(Seven, Spades),(Seven, Clubs),(Nine, Hearts),(Nine, Diamonds),(Nine, 
Spades),(Nine, Clubs),(Ten, Hearts),(Ten, Diamonds),(Ten, Spades),(Ten, 
Clubs),(Jack, Hearts),(Jack, Diamonds),(Jack, Spades),(Jack, Clubs),
(Queen, Hearts),(Queen, Diamonds),(Queen, Spades),(Queen, Clubs),(King, 
Hearts),(King, Diamonds),(King, Spades),(King, Clubs),(Ace, Hearts),(Ace,
Diamonds),(Ace, Spades),(Ace, Clubs)]"
```



