# Newtype declarations

A special case of a new type declaration `newtype` can be used **if the type has a single constructor with a single argument**. For example, a type for representing an IP address could be declared this way:

```haskell
newtype IPAddress = IP String
```

The `newtype` is different from `type` because it defines a completely new type rather than just a synonym for an existing type such as:

```haskell
type IPAddress = String
```

So any function that requires an `IPAddress` declared as a `newtype` will only work with that type, and not simply a `String` type.

When compared to `data`, the `newtype` has some efficiency benefits because it states that `IPAddress` is simply a wrapper for the value of an existing type `String`, whereas the data declaration:

```haskell
data IPAddress = IP String
```

states that `IPAddress` is a completely new data type.
