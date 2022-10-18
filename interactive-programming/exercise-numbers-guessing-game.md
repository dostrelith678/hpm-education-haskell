# Exercise - Numbers Guessing Game

Now that we know more about **actions** in Haskell, let's implement a number-guessing game between two players. The idea of this game is very simple and involves two players. The first player thinks of a number that must be hidden and the second player tries to guess it. If the guess is correct, the game ends, otherwise, the program outputs whether the wanted number is higher or lower than the guess, and asks for another guess.

We start by defining the high-level definition of the game itself in `Numbers.hs` which will have the type `IO ()`:

```haskell
numbers :: IO ()
numbers = do
  putStrLn "Think of a number: "
  number <- getSecretNumber
  putStrLn "Guess the number: "
  play number
```

Now, we just have to define our helper functions `getSecretNumber` and `play`. `getSecretNumber` should do two things. Firstly, it should only allow valid numbers (in our case integers) to be read, and secondly, it should not allow the entered number to be visible on the screen. Let's start with the first requirement and implement a `getInt` function – we have to tell Haskell that we want to read a line, but also that we must get a type `Int` out of it:

```haskell
getInt :: IO Int
getInt = do
  number <- getLine
  return (read number :: Int)
```

We use `getLine` to get input from the user, i.e. a string that is submitted once the new line character is entered, rather than just a single character as with `getChar`. And then, remember the [`Read` class](../type-classes/basic-classes/read-readable-types.md)? We know `Int` is an instance of the `Read` class so we can use the `read` method to read a `String` from `getLine` as an `Int`. We use the `:: Int` to explicitly state that we want to read an `Int` from the input. If that's not possible, we will get an exception, which is okay for now.

```haskell
ghci> getInt
10
10

ghci> getInt
abc
*** Exception: Prelude.read: no parse
```

As is, this function `getInt` can be used for guessing, but not for entering the number to be guessed. Now, for the second requirement, we must ensure that both the entering of a number is hidden when being entered. So we will also use the `hSetEcho` from the `System.IO` library to prevent printing to the screen while we read the number in our `getSecretNumber` function:

```haskell
getSecretNumber :: IO Int
getSecretNumber = do
  hSetEcho stdin False
  number <- getInt
  hSetEcho stdin True
  return number
```

Now, we have everything we need to define the `play` function, which represents the main game loop:

```haskell
play :: Int -> IO ()
play number = do
  putStr "? "
  guess <- getInt
  if | guess == number ->
         putStrLn "That's correct!"
     | guess > number ->
         do
           putStrLn "Too high!"
           play number
     | otherwise ->
         do
           putStrLn "Too low!"
           play number
```

We first ask for the guess and then use a [`MultiWayIf` ](../defining-functions-working-with-functions/conditionals/multiwayif.md)to decide what to print out and whether the game is finished. Don't forget that we must add the `{-# LANGUAGE MultiWayIf #-}` to the top of our `Numbers.hs` file for this to work. In the case of an incorrect guess, we print whether it is too high or too low and recursively call `play` again with the same secret number:

```haskell
ghci> numbers
Think of a number:
Guess the number:
? 9
Too low!
? 11
Too high!
? 10
That's correct!
```
