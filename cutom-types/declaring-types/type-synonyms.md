# Type Synonyms

**Type synonyms** are the simplest way to declare a new type as they simply provide an alias for one of the already existing types. For example, we already know that `String` is actually just a synonym for list of `Chars`, and it is defined as:

```haskell
type String = [Char]
```

We can use the declared type synonyms to define other types as well. We can define a type for a list of Strings:

```haskell
type StringList = [String]
```

It is important to note that the type synonyms and their base types are interchangeable in almost all cases. That means that any function that has a type signature including a list of strings \(`[String]`\) could be used on an element that has the type of `StringList` as they are just synonyms.

