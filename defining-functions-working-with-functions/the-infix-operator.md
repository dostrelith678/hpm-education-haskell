# The Infix Operator

This is a good time to introduce the **infix operator** that helps us make code a bit more readable. Normally, we apply a function by writing`FUNCTION> <ARGUMENT1> <ARGUMENT2>`, but we could also write it using the infix operator as`<ARGUMENT1> <FUNCTION> <ARGUMENT2>`. This way, we make the code more readable – for example, in the above case of`es = mod sum 2`, we can write:

```haskell
res = sum `mod` 2 -- using the infix operator ``
```

Which then reads as "`res` is equal to `sum modulo 2`". Note that the infix operator can be used this way for **functions that take in two arguments**. For functions with more than two arguments, we would need to add parentheses to explicitly create expressions \(which return another function – currying\):

```haskell
ghci> multiply x y z = x * y * z

ghci> (1 `multiply` 2) 3
6
```

