# Immutability

At this point in our training, you need to learn that all values in Haskell are immutable! But what does it mean for us? It means that when you apply a function to some variable, the value is not changed. Instead, you create a new value each time. That means assignment does not exist in Haskell.

```haskell
ghci> let a = [1,2,3]
ghci> reverse a -- reverse is a function that reverses a list
[3,2,1]
ghci> a -- the value of the expression "a" never changed
[1,2,3]
```

