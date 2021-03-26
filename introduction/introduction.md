# Introduction

Haskell is a purely functional computer programming language. To be more precise, it is a polymorphically- statically- and strongly-typed, lazy, compiled, purely functional programming language. We will explore what all of those mean soon enough, but let’s start by reviewing what are functions, what is functional programming and how functional programming differs from imperative programming.

### Functions

In Haskell, functions work exactly as they do in mathematics. In mathematics, functions define the unambiguous dependence of the output value to its arguments, i.e., they map the input values to the output. This means that for any combination of arguments, there can only be one result. Let’s look at a simple example of a function that takes one argument and multiplies it by three:

$$
f (x) = 3 * x
$$

 For any input value x, there is only one possible output:

$$
f (2) = 6
$$

$$
f ( -5) = -15
$$

This is exactly what we mean when we say Haskell is a purely functional programming language – because it focuses on pure functions whose output values are entirely determined by their arguments. This means that there are no side-effects to functions in Haskell, a function with the same arguments will always produce the same result no matter what else is going on in the program it is in, which make them very reliable.

In other words, Haskell functions do not allow anything besides simply taking inputs from their arguments and producing a return value, so things like printing on screen, reading from and writing to files are off the table for Haskell functions. However, that would mean Haskell cannot be very useful, and that is why it is still possible to integrate these important and useful features through the use of Monads \(we will not touch Monads for some time, but for now just trust me that Haskell can have very real applications – after all, Cardano is built with Haskell\).

In Haskell, we can define a function by using an equation that specifies:

1. The function name
2. The names of its arguments
3. The function body that specifies how the result will be calculated

To define our tripling function above in Haskell, we would write:

```haskell
triple x = 3 * x
```

where double is the function name, x is its only argument and 2 \* x is the function body. Notice that in Haskell, there are no parentheses that wrap around the arguments. The function name and the first argument, as well as any subsequent arguments, are simply separated by a space.

When the function is applied to actual arguments, the body of the function receives the arguments and the result is calculated \(with comments in curly parentheses\):

```haskell
triple 4
= { applying triple }
3 * 4
= { applying * } 
12
```

