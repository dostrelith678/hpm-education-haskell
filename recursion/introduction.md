# Introduction

In programming, we often want to repeat the same action multiple times, and this concept is called **looping**. Imperative languages have syntax for defining loops in their programs (usually in forms of `for` and `while`), and programming without loops is almost unimaginable. However, in Haskell, there is no such syntax for loops, and the **basic mechanism for looping is recursion**.

**Recursive functions** are those that are **defined in terms of themselves**, i.e. the function body includes a call to the function itself. This means that a function can call itself over and over again without stopping, creating an infinite loop. So when we define recursive functions, we usually include a special pattern that, when matched, does not call the function anymore but returns some value instead. This pattern is called **the base case**, while patterns that do call the function again are called **recursive cases**. Let's consider a simple function that calculates the sum of all natural numbers up to `n`:

```haskell
sumN :: Int -> Int
sumN 0 = 0                -- base case
sumN x = x + sumN (x - 1) -- recursive case
```

That is, the sum of all natural numbers up to zero is simply zero, and for any other integer `x`, it can be defined as the number `x` plus the sum of all natural numbers up to `x - 1`. Let's take a closer look at what the actual execution looks like:

```haskell
sumN 4
= 4 + sumN 3
= 4 + 3 + sumN 2
= 4 + 3 + 2 + sumN 1
= 4 + 3 + 2 + 1 + sumN 0
= 4 + 3 + 2 + 1 + 0       -- the base case stops further looping
10
```

Recursion is very powerful in Haskell when it is combined with lists. In fact, the `map` function we defined with a list comprehension is actually defined using recursion in the Prelude:

```haskell
map _ [] = []
map f (x:xs) = f x : map f xs
```

Like before, we have a base case in which we do not care about the function that is passed to map as the list it is supposed to operate on is empty and we simply return `[]`. The recursive case, however, applies the function `f` to `x` (the head of the list) and joins the result with the result of the recursive call on the remainder of the list (the tail of the list).
