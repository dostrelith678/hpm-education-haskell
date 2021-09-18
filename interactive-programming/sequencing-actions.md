# Sequencing Actions

Sometimes, we want to perform a sequence of actions one after the other. This can be easily done using the **do notation** in Haskell, which is used to create one composite action from two or more individual actions in the `do` block. The general structure of the `do` notation is the following:

```haskell
do value1 <- action1
   value2 <- action2
   ...
   return (value1, value2...)
```

We can read it as "perform `action1` that will generate the value `value1`, then perform the next action `action2` to generate the value `value2` and so on. In the end, return the tuple of generated values as a type `IO`." The `return` function is just another action in the sequence \(remember that `return` is a function by itself but when applied to an argument it returns an action\). That means that we do not have to use `return` at the end of the do block. We also do not have to use the generator arrow if we do not intend to use the result value from a particular action. For example, to write a simple `"Hello World"` program using do notation, we can use the `putStrLn` function, which prints a string to the screen and a new line character at the end of it:

```haskell
hello :: IO ()
hello = do
  putStrLn "Hello"
  putStrLn "World!"
  
ghci>hello
Hello
World!
```

