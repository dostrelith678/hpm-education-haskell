# Functional Programming vs Imperative Programming

Now that we took a look at functions in Haskell, let’s explore the concept of functional programming. In functional programming, the basic method of computation is the application of functions to arguments. Therefore, functional programming is best described as a style of programming, and functional programming languages support and encourage this style.

On the other hand, in imperative programming the basic method of computation is changing stored values, i.e. functions in imperative programming languages are not purely mathematical functions, but rather a sequence of instructions that the program should follow to get to the result. To better understand this, let’s see how a task of calculating the sum of natural numbers between `1` and `n` would normally be handled by an imperative language, C:

```c
int sum = 0;
for (i = 1; i <= n; i++) {
    sum = sum + i;
}
```

The above program first initialises a variable sum to zero, and then loops \(repeats the same action\) for all numbers from `1` to `n`, updating the stored value of  the `sum` variable on each iteration. In the case of `n = 3`:

```c
sum = 0;
{ first iteration }
i = 1;
sum = 1;
{ second iteration }
i = 2;
sum = 3;
{ third iteration }
i = 3;
sum = 6;
```

Now let's take a look at how that task could be handled by Haskell – we can achieve this with a combination of two functions:

1. `[n .. m]` – which produces a list of numbers from `n` to `m`, e.g. `[1..3] => [1, 2, 3]`
2. `sum`  – which produces the sum of a list

{% hint style="info" %}
`sum` is a predefined function in the Haskell standard library, called Prelude, which is imported by default into all Haskell modules. Libraries are collections of functions written by other people to solve various problems that we can use without having to write them ourselves.
{% endhint %}

```haskell
sum [1..3]
= { applying [..] }
sum [1, 2, 3]
= { applying sum }
1 + 2 + 3
= { applying + }
6
```

The above example shows that executing Haskell programs triggers a sequence of function applications – the basic method of computation in functional programming. In functional programming, the code tells the program what to calculate, but not explicitly how to get to the end result following a sequence of steps.

That brings us to another important thing – there are no variable assignments in Haskell. The equality sign `=`  in Haskell is not the assignment operator as in imperative languages, but the equivalent of the mathematical equal sign.

