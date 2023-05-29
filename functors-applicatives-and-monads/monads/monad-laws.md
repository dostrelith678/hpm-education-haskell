# Monad Laws

There are three laws that monad instances must satisfy to be valid:

* Left Identity ->  `(return x) >>= f = f x`

The left identity law states that if we simply use `return` on a value before binding it to the function `f`, the result should be the same as simply applying `f x` directly.

* Right Identity -> `m >>= return = m`

The right identity law states that if have some monadic value `m` (or an expression that computes to this monadic value) and bind it to the `return` function, the result should be simply the same value `m`.

* Associativity -> `(m >>= f) >>= g = m >>= (\x -> f x >>= g)`

The associativity law states that if have some monadic value `m` and want to create a chain binding for functions `f` and `g` (applying `f` first, and the result of that application to `g`), then it should not matter whether we nest the two binding functions, as long as the order of application is preserved.

