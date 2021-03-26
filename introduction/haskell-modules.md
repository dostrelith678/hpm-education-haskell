# Haskell Modules

Haskell code is organised into modules, which are files that contain the source Haskell code. Each module corresponds to one single file, and the standard extension for Haskell modules is `.hs`. Each module should start with the name of the module which is also the same name of the corresponding file, e.g. module `Triple.hs`:

```haskell
module Triple -- module name
(
    triple -- module interface (what is explicitly exported)
) where

{- Module contents -}
triple x = 3 * x -- function declaration
```

First, we have the module name `Triple`, followed by the module interface wrapped in parentheses. The module interface states what gets exported from this module, i.e. if this module is imported somewhere else, the`triple`function is the only thing that would be usable from this module. If we had another function declared in the module contents \(e.g. `quadruple`\), that function would not be exported unless specified in the module interface.

However, the module interface is optional, and if omitted, all the declarations from the module will be exported. Comments serve the purpose of documenting our code and anything we put in comments will not be evaluated in the program. Haskell comments can be single-line and multi-line – single-line comments start with `--`, and multi-line comments are wrapped between `{- -}`. Any comments in this guide will also follow the same format.

