# Folds

A **fold** or a **folding function** is a higher-order function that processes a data structure (e.g. a list) in some order and builds a return value along the way. Therefore, a fold needs three things to work - **a function that combines the elements, a starting value, and the data structure** where the elements are stored.

There are two basic folding functions defined in the Haskell Prelude, `foldr` and `foldl`. The difference between them is the order in which they apply the combining function to the elements.

