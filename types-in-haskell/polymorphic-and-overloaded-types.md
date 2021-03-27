# Polymorphic and Overloaded Types

We have already touched upon **polymorphic types** in our`triple`function when we made it possible to triple both integers and floating-point numbers. We used`Num a`in the **function's type signature** to specify that it can accept both number types as arguments. The `Num` is a class constraint and `a` is the **type variable** and our function signature `triple :: Num a => a -> a` reads as "for any type `a` that is an instance of the **class `Num`**, the function `triple` has the type `a -> a`".

Any type that has a **class constraint** is called an **overloaded type**, and hence our`triple`function is an **overloaded function**. We can even also specify a **type variable** without the class constraint, in which case that type is **completely polymorphic** and any type can fill the arguments' place. For example, this is used in several list functions we used earlier, as their results do not depend on the types of elements that fill the lists. For example, the `head` \(return the first element of a list\) and `tail` \(return the list excluding the first element\) functions must work regardless of what type the elements in the list are. Therefore, their type signatures are:

```haskell
head :: [a] -> a
-- a list of type a's returns a type a, whatever type a is for that list

tail :: [a] -> [a]
-- a list of type a's returns a type [a], whatever type a is for that list
```

