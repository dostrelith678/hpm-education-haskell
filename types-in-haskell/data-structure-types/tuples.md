# Tuples

**Tuples**, unlike lists, can contain elements of **different types**. The elements of a tuple are enclosed in round parentheses and separated by commas:

```haskell
("Cardano", True) :: (String, Bool)
```

The above is an example of a **tuple pair** that is comprised of two elements, in this case, a string and a boolean. Notice that the tuple type is dependent on its elements – both the number of elements and their individual types. Unlike with lists, where we have one clear type for any single list regardless of its length, tuples must be finite and the type of each element must be known in order for the Haskell type system to able to work properly. The length of a tuple is sometimes referred to as its **arity**.

```haskell
[1] :: [Int] -- The type of the list is the same...
[1, 2, 3] :: [Int] -- ...regardless of its length.

(1, 2) :: (Int, Int) -- The type of the tuple changes...
(1, 2, False) :: (Int, Int, Bool) -- ...with its length (and element types).
```

**Tuples** are most commonly used as key-value pairs – a data structure for storing and retrieving data. That is why I said **pairs** are the most common of tuples – for example, a name–address pair or a dictionary word-definition pair.
