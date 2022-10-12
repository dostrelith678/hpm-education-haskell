# List Comprehensions

In this chapter, we introduce **list comprehensions**, which are used to create new lists from existing ones. The term comes from mathematics, where _set comprehension_ is used to describe a set by enumerating its elements and/or stating conditions its members must satisfy. In Haskell, the syntax is the following:

```haskell
[ <GENERATOR> | <ELEMENT> <- <LIST>, <GUARD> ]
```

The `GENERATOR` is an expression that specifies how the elements of the new lists should be calculated, the `ELEMENT` is an element from the specified existing `LIST`, and the `GUARD` is **an optional condition** we can set that an `ELEMENT` must satisfy to end up in the new list we are creating via the `GENERATOR` expression. The whole line can be read as _"create a list by applying the `GENERATOR` for each `ELEMENT` of the `LIST` that meets the criteria set by the `GUARD`"_. Let's take a look at an example list comprehension that creates **a list of only even numbers**:

```haskell
ghci> [x | x <- [1..10], even x]
[2,4,6,8,10]
```

The above can be read as _"create a list of all numbers `x` such that `x` is an element of the list `[1..10]` and `x` is an even number"_. This simply puts `x` into a new list if it meets the guard criteria, but we could also apply function(s) to `x`:

```haskell
ghci> [x * 2 | x <- [1..10], even x]
[4,8,12,16,20]
```

We do not even have to use `x` for our generator, while we can still use it for the guard expression:

```haskell
ghci> ["even!" | x <- [1..10], even x]
["even!","even!","even!","even!","even!"]
```

We can also specify **multiple lists as well as multiple guards in list comprehensions**. In the case of multiple lists, the deeper nested list (the one specified last) is iterated through for each element of the previous list(s):

<pre class="language-haskell"><code class="lang-haskell">ghci> [ (x, y) | x &#x3C;- [1..3], y &#x3C;- ['a'..'c'] ]
[
<strong>    (1,'a'),(1,'b'),(1,'c'),
</strong>    (2,'a'),(2,'b'),(2,'c'),
    (3,'a'),(3,'b'),(3,'c')
]</code></pre>

In this case, the list `['a'..'b']` is iterated through three times, once for each element in the first list `[1..3]`.
