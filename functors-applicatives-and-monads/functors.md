# Functors

**Functors **_****_ generalise the idea of function mapping on a data structure type, i.e. applying a function to each element in the data structure. We have looked at the `map` function that does exactly that but is limited to a specific data structure - `list`. However, any **parameterised **_****_** type **_****_ (data structure) can be made into an instance of the `functor` class so that it supports function mapping to its elements through the use of the `fmap` function:

```haskell
class Functor f where
  fmap :: (a -> b) -> f a -> f b
  (<$) :: a -> f b -> f a
  
  -- Minimal complete definition:
  -- fmap
```

{% hint style="info" %}
The `(<$)` function simply replaces all elements in the data structure with the given value `a.`
{% endhint %}

Comparing `fmap` to `map`:

```haskell
map :: (a -> b) -> [a] -> [b]
```

We can see that `fmap` has the exact same type signature as `map` - but`map` is limited to the type of `lists`, whereas `fmap` can be used with any parameterised type that uses a type constructor`f`. Note that form of`[a]` and `[b]` is just syntax sugar for the list type and is equivalent to `[] a` and `[] b` , where `[]` is the _type constructor_ for lists.

Since the `map` and `fmap` function perform the same action, it is very simple to make the `list` type into a functor (and it is made into one by default):

```haskell
instance Functor [] where
    -- fmap :: (a -> b) -> [] a -> [] b
    fmap = map
```

However, when it comes to other data structure types, we have to define the `fmap`  function ourselves. For example, the Maybe type (also an instance of the Functor class by default) and can be made an instance as:

```haskell
instance Functor Maybe where
    -- fmap :: (a -> b) -> Maybe a -> Maybe b
    fmap _ Nothing = Nothing
    fmap f (Just x) = Just (f x)
```

In the case of a `Nothing`, we ignore the function and just return `Nothing` as `Nothing` in general represents an error state that we then want to propagate through our `fmap` function as well. Otherwise, we apply the function `f` to the underlying value `x` of `Just x` and return the Maybe type (using the `Just` constructor) of the result.

Now let's see how we can make a newly-defined data type into an instance of the Functor class. We will first define a data type `Tree` that will represent a **full binary tree** ([https://en.wikipedia.org/wiki/Binary\_tree](https://en.wikipedia.org/wiki/Binary\_tree)). A full binary tree is a binary tree type in which every tree node has either `0` or `2` children. In the case of a node with `0` children, it will be a `Leaf` that stores some value, and in the case of a node with `2`  children, it will be a `Branch` that branches into two new nodes:

```haskell
data Tree a = Leaf a | Branch (Tree a) (Tree a)
                deriving (Show)
```

And now, we want to make `Tree` a functor, so we have to define the `fmap` function for it:

```haskell
instance Functor Tree where
    -- fmap :: (a -> b) -> Tree a -> Tree b
    fmap f (Leaf x) = Leaf (f x)
    fmap f (Branch l r) = Branch (fmap f l) (fmap f r) 
```

The first case of `Leaf` is analogous to how we defined the `Just` case of the `Maybe` functor - we apply the function `f` to the underlying value `x` and return it wrapped in the `Leaf` constructor. In the other case, where we are dealing with a `Branch` we recursively apply `fmap` to both children nodes of the branch.

To represent the following binary tree:

![](../.gitbook/assets/binary\_tree.png)

We can use the following code and `fmap` over the entire data structure, applying the passed function to each leaf:

```haskell
ghci> myTree = (Branch (Branch (Leaf 1) (Leaf 2)) (Branch (Leaf 10) (Leaf 20)))
ghci> fmap (/2) myTree

Branch (Branch (Leaf 0.5) (Leaf 1.0)) (Branch (Leaf 5.0) (Leaf 10.0))
```

Note that the `Prelude` comes with an infix operator for `fmap` as well - `(<$>)`:

```haskell
 ($)  ::              (a -> b) ->   a ->   b
(<$>) :: Functor f => (a -> b) -> f a -> f b
(<$>) = fmap
```

`($)` is the simple function application operator we learned about before, while `(<$>)` is also a function application operator but with lifting over a Functor. We could also write the above code as:



```haskell
ghci> myTree = (Branch (Branch (Leaf 1) (Leaf 2)) (Branch (Leaf 10) (Leaf 20)))
ghci> (/2) <$> myTree

Branch (Branch (Leaf 0.5) (Leaf 1.0)) (Branch (Leaf 5.0) (Leaf 10.0))
```

## Functor Laws

There are two functor laws that must be satisfied and ensure that `fmap` works as intended:

```haskell
fmap id = id
```

The `id` is the identity function, and it used to simply return the unaltered argument passed in. This means that mapping the `id` function over a structure should return the same structure back unaltered.

```haskell
fmap (g . f) = fmap g . fmap f
```

The second functor law ensures that _function_ _composition_ is preserved when using `fmap` so that it does not matter whether we map a composed function `(g . f)` or map the first function `g` and then the second function `f`, as long as the order of the `g` and `f` functions stays the same.
