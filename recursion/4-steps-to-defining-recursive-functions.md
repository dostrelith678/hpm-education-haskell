# 4 Steps to Defining Recursive Functions

A good set of steps to follow when defining recursive functions is:

1.  **Define the function type**

    Thinking about function types is very helpful when defining functions, and explicitly

    defining the function type is good practice.
2.  **Enumerate different cases**

    Considering the general cases we expect allows us to create the function structure that we can then fill out gradually. For example, two standard cases for lists are empty and non-empty lists.
3.  **Take care of the simple cases first (usually base cases)**

    The simple cases are usually straightforward so it's easier to define them. For example, our

    `sumN 0 = 0` is a simple case and also the base case.
4.  **Define the other cases**

    Here, we have to think about how to calculate the wanted result using both the recursive call

    on the function itself and any other functions we might need. For example, in `sumN x = x sumN (x - 1)` we used both the `(+)` and `(-)` functions.



