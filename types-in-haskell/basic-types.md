# Basic Types

## Bool – logical values 

**Bool** is a logical data type that can be either `True` or `False`.

## Int – fixed-precision integers

**Int** can contain integers, whole numbers both negative and positive \(e.g. `-50`, `50`\) up to a certain size which is limited by a fixed amount of memory, hence the term fixed-precision. GHC can hold values in the range of `(-2^63)` to `(2^63 - 1)` for Int types - going outside those ranges will yield unexpected results.

## Integer – arbitrary-precision integers 

**Integer** is the same as Int except it does not have a limit to the values it can hold. Performance-wise, it is better to use Int if we know our values will not go out of range, as most computers have built-in hardware for dealing with fixed-precision integers.

## Float – single-precision floating-point numbers 

**Float** can contain decimal numbers \(e.g. `-1.5`, `6.23`, `50.0`\) up to a certain precision which is limited by a fixed amount of memory. The term floating-point comes from this memory limitation, which limits the number of digits \(precision\) that can come after the decimal point based on the size of the number.

## Double – double-precision floating-point numbers

**Double** is the same type as float, containing decimal numbers but with double the memory assigned for storage, increasing their precision. 

## Char – single character

**Char** is a type for characters – it can hold any Unicode character including control characters such as `'\n'` \(a new line character\) or `'\t'` \(tab stop character\). Chars must be enclosed in single quotes `' '`. 

## String – strings of characters

**Strings** simply hold a string of characters – they are in fact a type `[Char]` \(a list of characters\) in Haskell. Strings must be enclosed in double-quotes `" "`, e.g. `"Haskell is great"`.

