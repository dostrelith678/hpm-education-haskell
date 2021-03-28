# Eq – Equality Types

The `Eq` class supports the comparison methods \(equality and inequality\), so any two values of a type that is an instance of the `Eq` class can be compared using the functions:

```haskell
(==) :: a -> a -> Bool
(/=) :: a -> a -> Bool
```

We have already used these functions many times, and we were able to because all the basic types \(`Char`, `Bool`, `Int`....\) are instances of the `Eq` class. Classes are defined using the `class` keyword followed by the class name, the type specification and the where keyword, followed by the default definitions of the class methods:

```haskell
class Eq a where
  (==), (/=) :: a -> a-> Bool
  
    -- Minimal complete definition:
    -- (==) or (/=)
    
  x /= y = not (x == y)
  x == y = not (x /= y)
```

We see the two default methods defined in terms of each other, which means we need to define one of them in a clear way to have a complete definition for an instance. For example, the `Bool` type can be made an instance of the `Eq` class with:

```haskell
instance Eq Bool where
  False == True = False
  True == False = False
  _ == _ = True
  
-- or using the (/=) method
    
instance Eq Bool where
  False /= True = True
  True /= False = True
  _ /= _ = False
```

Keep in mind that the definitions of the required functions can be as simple or as complicated as you like, and default definitions can be overwritten when declaring instances.

