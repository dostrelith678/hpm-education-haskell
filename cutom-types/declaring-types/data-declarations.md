# Data Declarations

With the keyword `Data`, we can define new types rather than just synonyms for already existing ones. Types declared with `data` are called **algebraic**, referencing **"sum"** and **"product"**. In data types, **"sum"** means _alteration_ (`A | B`, meaning `A` or `B` but not both), and **"product"** means _combination_ (`A B`, meaning `A` and `B` together).

For example, we can create a type that represents a card suit:

```haskell
data Suit = Hearts
          | Diamonds
          | Spades
          | Clubs
```

`Suit` is the **type constructor** in this definition, and the values (`Hearts`, `Diamonds`, `Spades` or `Clubs`) are **data constructors**. It states that the new type `Suit` can have **one of the four values** (the `|` symbol stands for "or"). This means that `Suit` is a **sum type**, which is any type that has multiple possible representations. Another example of a sum type would be `Bool` which can be either `True` or `False:`

```haskell
data Bool = True | False
```

**Data constructors** can have zero or more arguments. `Hearts | Diamonds` and `True | False` are examples of data constructors that have zero arguments - **nullary data constructors**. Likewise, **type constructors** can have zero or more arguments. `Suit` and `Bool` are examples of **nullary type constructors**.

Let's take a look at some type- and data- constructors that have more than zero arguments. Here is an example of an error type from the [cardano-node repository](https://github.com/input-output-hk/cardano-node/blob/85d05720da7b0c02dfa890079e568c8499a027a7/cardano-node/src/Cardano/Node/Types.hs#L49-L52):

```haskell
data ConfigError =
    ConfigErrorFileNotFound FilePath
  | ConfigErrorNoEKG
    deriving Show
```

`ConfigError` is a nullary type constructor, and its data constructors are `ConfigErrorFileNotFound FilePath`, and `ConfigErrorNoEKG`. `ConfigErrorFileNotFound FilePath` is a **unary** data constructor meaning that it actually holds some data, in this case of type `FilePath`. Nullary type constructors we have seen so far contain no data aside from their names.

Both the type name and its constructors must begin with a capital letter, and **constructors must be unique** to that type, i.e. the same constructor cannot be defined in more than one type. Once a new type is defined, it can be used in functions just like any other data type in Haskell. To illustrate, a very simple function to get the card suit in a string format using pattern matching would be:

```haskell
suitStr :: Suit -> String
suitStr Hearts = "... of hearts."
suitStr Diamonds = "... of diamonds."
suitStr Spades = "... of spades."
suitStr Clubs = "... of clubs."

ghci> suitStr Hearts
"... of hearts."
```

