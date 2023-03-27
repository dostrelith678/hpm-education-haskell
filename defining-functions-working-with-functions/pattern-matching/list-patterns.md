# List Patterns

As with tuple patterns, we can think of list patterns as a combination of two types of patterns as well. The first type is the patterns for each individual element we define which forms a list of patterns. The second type comes from the fact that that same list of patterns is a pattern itself. For example, let's say we want to define a function that takes in a list of any type and checks whether it contains exactly 4 elements:

```haskell
check4 :: [a] -> Bool
check4 [_, _, _, _] = True
check4 _ = False
```

That is, we first check the pattern of `[_, _, _, _]`, which is a list of four patterns itself, one for each individual element in the expected list, and for each of those we use the wildcard because we do not care about what the value of the element is. We only care that the element exists there and that there are exactly four elements in the list. If that first pattern doesn't match, we simply use the wildcard to say that whatever is there, we already know it does not contain exactly 4 elements and return `False`.

But there is also another list pattern that is very useful and it takes advantage of the cons `(:)` constructor used for constructing lists. We know [from before](../../types-in-haskell/data-structure-types/lists/list-functions.md) that a list represented as `[1, 2, 3]` is actually constructed as `1 : 2 : 3 : []` using the `(:)` constructor, so we can use that form in our list patterns (but we must parenthesise patterns using cons):

```haskell
check4 :: [a] -> Bool
check4 (_ : _ : _ : _ : []) = True
check4 _ = False

ghci> check4 [1,2,3]
False
ghci> check4 [1,2,3,4]
True
```

In fact, we can represent any list **with at least one element** with the following pattern:

```haskell
(x : xs)
```

In this pattern, `x` is **the first element** of the list and `xs` is **the tail of the list** (whatever remains after excluding the first element). The `xs` can be a list of `n` number of elements or it could even be just an empty list `[]`, in which case, the whole expression `(x : xs)` would be a list of just one element. Note that `x` and `xs` are simply standard names in this pattern, but we could use other names if we'd like to.

This means we can **pattern match on lists with an undefined number of elements**, unlike with tuples, where we have to match a finite number of elements. For example, the list functions `head` and `tail` use exactly this pattern to select the first element and the tail of a list, respectively:

```haskell
head :: [a] -> a
head (x : _) = x

tail :: [a] -> [a]
tail (_ : xs) = xs
```

We said that the pattern `(x : xs)` holds true for any list with at least one element, so what happens if we call these functions on an empty list?

```haskell
ghci> head []
*** Exception: Prelude.head: empty list

ghci> tail []
*** Exception: Prelude.tail: empty list
```

That case is covered by throwing an error since empty lists have neither a head nor a tail.
