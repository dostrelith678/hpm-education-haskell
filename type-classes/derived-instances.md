# Derived Instances

The deriving keyword can be used to make a new type into an instance of other built-in classes `Eq`, `Ord`, `Show`, `Read`, and `Enum` without the need for defining any of the methods. For example, the `Bool` type can be declared as:

```haskell
data Bool = False | True
  deriving (Eq, Ord, Show, Read)
```

It is as if we are stating that the new data type `Bool` can have two values (two nullary constructors `True` and `False`) and it should also be made an instance of the classes `Eq`, `Ord`, `Show` and `Read`, but we let the compiler write the actual code for us using the default definitions. Note that for the `Ord` class, the default ordering will be the order in which the constructors are defined – in this case, `True` comes after `False` and is, therefore _"greater than"_ `False`. With this definition, we can use methods of all the class instances included with the type `Bool`:

```haskell
ghci> True == True
True

ghci> False < True
True

ghci> show True
"True"

ghci> read "False"
False
```
