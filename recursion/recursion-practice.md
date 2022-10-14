# Recursion Practice

Let's practice recursion by defining some more recursive functions:

* A function that takes two positive integers, `x` and `y` and **raises `x` to the power of `y`** :
  1.  **Define the type**

      We know the function will take two integers and return an integer.

      ```
      power :: Int -> Int -> Int
      ```
  2.  **Enumerate different cases**

      We can think of two special cases, where either of the arguments is zero, and the general case where both are greater than zero.

      ```
      power _ 0 =
      power 0 _ = 
      power x y =
      ```
  3.  **Take care of the simple cases first (usually base cases)**

      Any number to the power of zero is equal to one. Note that we set this pattern first

      because we want to consider zero to the power of zero to be equal to one. The other simple case is that zero to the power of any other number (other than zero itself) is equal to zero.

      ```
      power _ 0 = 1
      power 0 _ = 0
      ```
  4.  **Define the other cases**

      Now, we get to the recursive case. We can define that `x` to the power of `y` is equal to `x`

      multiplied by the result of the recursive call to the function with `(y - 1)`

      ```
      power x y = x * power x (y -1)
      ```

{% hint style="info" %}
For practice, write out how this function would be applied step by step. &#x20;
{% endhint %}

* A function that takes in a list and **returns a new list with only the even-indexed** **elements** (with the first element considered odd-indexed):
  1.  **Define the type**

      We know the function will take in a list of some type and return a list of the same type.

      ```
      evens :: [a] -> [a]
      ```
  2.  **Enumerate different cases**

      Here, we have to think about the cases we can have. The first one is very simple, if the supplied list is empty, we should return an empty list, but we will leave the definitions for what to return for the next step. The next case we can consider is a list with only one element. We are then left with the general case of two or more elements in a list.

      ```
      evens [] = 
      evens [_] = 
      evens (_ : x : xs) = 
      ```
  3.  **Take care of the simple cases first (usually base cases)**

      In the first case (empty list) we already mentioned that we just want to return an empty list. The case with just one element in the list should also return an empty list as that element is odd-indexed and we are only interested in even-indexed elements.

      ```
      evens [] = []
      evens [_] = []
      ```
  4.  **Define the other cases**

      That last case we laid out is where the list has two or more elements. In this case, we should ignore the first element, take the second one and join it with the result of the recursive call of the remaining list.

      ```
      evens (_ : x : xs) = x : evens x
      ```

{% hint style="info" %}
For practice, write out how this function would be applied step by step. &#x20;
{% endhint %}

