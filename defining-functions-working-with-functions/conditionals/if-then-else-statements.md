# If-then-else Statements

The syntax in Haskell for if-then-else statements is:

```haskell
if <CONDITION> then <EXPRESSION1> else <EXPRESSION2>
```

where the `CONDITION` must be a **boolean expression**. If the condition evaluates to `True`, then `EXPRESSION1` is used, otherwise, `EXPRESSION2` is used. One other thing to note here is that **both expressions in the if statement must be of the same type**. For example, the statement:

```haskell
if True then 1 else 'untrue'
```

is invalid because the type of `1` is `Int`, but the type of `'untrue'` is `String` \(synonym for `[Char]` - a string is simply a list of characters\).

Let's take a look at a simple example function using a conditional statement to decide on its result for a score on a race track given two arguments – the time achieved and the average time for the track in seconds:

```haskell
trackScore :: Float -> Float -> String
trackScore time avgTime =
  if time < avgTime
  then "Great! Your time is " ++ show (avgTime - time) ++ " seconds 
    below average!"
  else "Your time is " ++ show (time - avgTime) ++ " seconds above 
    average."
```

You have probably noticed this new function `show` – it is a method \(function\) from the `class Show` and it is used to represent the value of a type as a string. Hence, it has the following type signature:

```haskell
show :: a -> String
```

{% hint style="info" %}
We will explore classes in more detail later on - for now, just know that a `class` comes with certain **methods** \(functions\) it supports.
{% endhint %}

All the basic types \(`Bool`, `String`, `Char`, `Int`, `Integer`, `Float` and `Double`\) are instances of the `Show` class which enables us to use the `show` function and get their representation as a string:

```haskell
ghci> show 252.5
"252.2"
```

In our function `trackScore`, we consider the two cases where the given time is lower than the average time and when it is higher than the average time. But what if it is exactly the same?

```haskell
ghci> trackScore 10 10
"Your time is 0.0 seconds above average."
```

The output is not wrong, but ideally, we would like to see some third version of output for this particular case. We could nest another if statement in our existing code and write:

```haskell
trackScore :: Float -> Float -> String
trackScore time avgTime =
  if time < avgTime
    then "Great! Your time is " ++ show (avgTime - time) ++ " seconds 
      below average!"
    else 
      if time == avgTime
        then "Your time is on par with the average time!"
        else "Your time is " ++ show (time - avgTime) ++ " seconds above 
          average."
      
ghci> trackScore 10 10
19"Your time is on par with the average time!"
```

The output is fine now, but with every **nested if-statement**, the code gets harder to read. Turns out there is a way to make it look nicer – **MultiWayIfs**.

