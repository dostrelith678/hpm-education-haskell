# Data Declarations

With the keyword `Data`, we can define new types rather than just synonyms for already existing ones. Types declared with `data` are called **algebraic**, referencing **"sum"** and **"product"**. In data types, **"sum"** means _alteration_ (`A | B`, meaning `A` or `B` but not both), and **"product"** means _combination_ (`A B`, meaning `A` and `B` together).

### Sum-types

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

### Product-types

The `Suit` type is an example of a sum-type. Now let's look at an example of a product-type that combines multiple fields together. We can imagine a rectangle, which has two sides `a` and `b`, and to construct a valid rectangle both of them must be provided. We can define the type as:

```haskell
data Rect = Rect Double Double
    deriving Show
```

In this case, the `Rect` on the left side is the type constructor (nullary), and the `Rect` on the right side is the data constructor (binary as it takes two arguments). To create a valid `Rect` type, both `Double` arguments must be joined together:

```haskell
ghci> a = Rect 2.0 3.0
ghci> a
ghci> Rect 2.0 3.0
```

It is interesting to note that the `Rect` on the right side is a function:

```haskell
ghci> :type Rect
ghci> Rect :: Double -> Double -> Rect
```

This means that even here we can take advantage of partial application:

```haskell
ghci> a = Rect 2.0
ghci> :type a
ghci> a :: Double -> Rect
```

And we can create functions based on the `Rect` type, for example, calculating the rectangle area:

<pre class="language-haskell"><code class="lang-haskell">area :: Rect -> Double
area (Rect a b) = a * b

<strong>ghci> area Rect 2.0 3.0
</strong>ghci> 6.0
</code></pre>

### Field labels (records)

As you can imagine, with product-types that represent more complex things, such as people or any large set of parameters, the definitions might become unclear from just the list of the arguments in the type. For example, imagine a type to define a company. We would need fields for e.g. the company name, its address, year of foundation, number of employees...

```haskell
data Company = Company String String Int Int
```

From the above definition alone, it is hard to intuitively understand which `String` or `Integer` stands for what. A more intuitive way to define complex types is by using the **field labels**:

```haskell
data Company = Company {
    cName :: String,
    cAddress :: String,
    cYear :: Int,
    cNre :: Int
} deriving Show
```

This is much more user-friendly. In addition, by using field labels, we get automatic _getter_ functions for individual fields:

```haskell
ghci> c = Company "MyCompany" "25th Street" 1999 26
ghci> cAddress c
"25th Street"
ghci> cYear c
1999
```
