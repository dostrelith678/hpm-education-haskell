# Immutability

At this point in our training, you need to learn that all values in Haskell are immutable! What exactly does that mean? It means that when you apply a function to some argument, the value of that argument cannot be changed. Instead, you create a new value each time. That means "variable assignment" does not exist in Haskell. Instead, we only assign a _name_ to an expression and we know that that _name_ will always evaluate only that expression.

```haskell
ghci> let a = [1,2,3]
ghci> reverse a -- reverse is a function that reverses a list...
[3,2,1]
ghci> a -- ...but the value of the expression "a" never changes
[1,2,3]
```
