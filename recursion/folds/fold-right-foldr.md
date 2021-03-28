# Fold Right \(foldr\)

The `foldr` function associates the combining function to the right, i.e. the right-most elements of the data structure will be evaluated first. Let's take a look at its definition using recursion on lists:

```haskell
foldr :: (a -> b -> b) -> b -> [a] -> b
foldr f v [] = v
foldr f v (x:xs) f x (foldr f v xs)
```

The starting value `v` is used to complete the folding once we get to the end of the list. Otherwise, we would be missing one last argument and get a curried function as a result instead of the value we are looking for. The case of a non-empty list is handled by simply applying the function `f` to the head of the list, and the recursively processed tail \(as we know the function `f` takes in two arguments\). Two simple examples of folding would be calculating the sum and product of a list:

```haskell
sum :: Num a => [a] -> a
sum xs = foldr (+) 0 xs
```

Where `(+)` is our combining function and `0` is the starting value. The application would look like this:

```haskell
sum [1, 2, 3]
1 + (foldr (+) 0 [2, 3])
1 + (2 + (foldr (+) 0 [3]))
1 + (2 + (3 + (foldr (+) 0 [])))
1 + (2 + (3 + 0))
6
```

Here, it is clear that the function application associates to the right. We can also see that the application of `foldr` can be thought of as replacing the cons operator in the list with our combining function \(in this case the addition operator\):

```haskell
[1, 2, 3]
1 : (2 : (3 : [])) -- list construction
1 + (2 + (3 + 0)) -- foldr (+)
```

And to define a function that calculates the product of a list using `foldr`:

```haskell
product = foldr (*) 1
```

In this case, our starting value is `1` instead of `0` as we are dealing with multiplication and not addition. Also, note that we have taken `xs` out of the definition from both sides of the equation – this is called **eta reduction** and is used to simplify functions. It takes advantage of partial application of functions so that the function product now returns a curried version of `foldr` that takes in one final argument \(the data structure\) to be completely applied. It is important to note that the type of the function does not change in its reduced form.

```haskell
product [1, 2, 3]
1 * (foldr (*) 1 [2, 3])
1 * (2 * (foldr (*) 1 [3]))
1 * (2 * (3 * (foldr (*) 1 [])))
1 * (2 * (3 * 1))
6
```



