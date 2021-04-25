# Applicative Functors

The missing functionality of functors is obvious - `fmap` only works for functions that take in exactly 1 argument and applies that function to each individual element of a given data structure. But we might want to apply a function that takes multiple arguments. For example, recalling our binary tree from the last page, what if we didn't want to alter each element of the tree, but instead calculate the sum of all nodes? Of course, we could define a function to deal with our specific case:

```haskell
sumTree :: Tree Int -> Int
sumTree (Leaf x) = 
addMaybe _ _ = Nothing
```

But there is a better way through the use of **applicative functors** or **applicatives** that generalise the idea of function application 

