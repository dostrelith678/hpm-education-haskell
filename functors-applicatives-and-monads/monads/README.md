# Monads

{% hint style="info" %}
This section is still a work in progress.
{% endhint %}

#### About Monads

Let's start by saying that monads are difficult to grasp at first. It might take you some time and a couple of attempts to really understand them, so don't worry if they seem overwhelming at the start. Like functors and applicatives, monads provide an abstraction for chaining operations that allows us to structure our programs generically and avoid code duplication. This abstraction allows us to simplify problems like handling exceptions during execution \(which we will explore shortly\) by building succinct pipelines without needing to worry about control flow or side-effects.

Many types we already encountered as pre-defined in Haskell are also instances of the `Monad` typeclass, including `Maybe` and `List`.

