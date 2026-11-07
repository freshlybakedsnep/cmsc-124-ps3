# Reasoning for the Predictions Table

Write one entry under every heading below, then commit this file together with
`predictions.tsv`, before you run a case or open `tests/expected.tsv`.

Each entry names the rule that produces the four predicted fields for that
case. One to three sentences is enough. The grader checks structure only. It
does not judge quality, and it sets no word minimum.

After you run the cases, add a short correction under each case you predicted
wrongly. Say what you predicted, what CLISP printed, and which rule you
misread. Those entries belong in the correction commits.

## P01
`+` and `*` are functions as defined by LISP. Each element is evaluated first before the function is executed (`+` then `*`).  

## P02
`QUOTE` or `'` returns an object unevaluated. It is a special-operator according to the glossary.
correction: miscounted length of list

## P03
`NIL` is a symbol that represents an empty list, false, and the null type. 

## P04
`t` is a symbol that represents the truth boolean value.  

## P05
`SYMBOLP` returns a generalized boolean, `true` if object is of type symbol; `false` if otherwise. `NIL` is a symbol, therefore `SYMBOLP` returns true or in this case `t`

## P06
Returns the  first argument of a `cons`. The list is empty, therefore returns the `nil` symbol.
correction: listed operator was for the produced `NIL` symbol instead of the `CAR`'s

## P07
A function that creates a new `cons` object. Flattens sub-lists into the new generated list.

## P08
Special-operator `IF` evaluates the expression: selects the `then-form` if true; otherwise `else-form` is selected. Whichever selected form is evaluated and returned. 
correction: listed operator was for the produced symbol instead of the expression

## P09
`AND` evaluates each form one at a time from left to right. If all forms are true values, returns the results produced by evaluating the last form. Otherwise, short-circuits and returns `NIL`. Since a form here is not a true value, it returns `NIL`.
correction: listed operator was for the `NIL` symbol returned after evaluation instead of the `AND`'s

## P10
Special operator `PROGN` evaluates forms in the order they are given. `DEFVAR` and `DEFFUN` are built-in lisp implementations (macros) for variable and function declaration. Accessing variables wrapped with `*` returns its most recent value. Therefore, ps3-scale uses the most recent ps3-rate value (10) and evaluates to 30. 

## P11
`DEFUN` is a macro that returns an object of the function declared; it returns a symbol that acts as identifier which binds the defined function to the object. 

## P12
Special operator `labels` defines and executes a function whose scope encompasses only within the body and returns the last expression evaluated. `down` defined here is a recursive local function, which returns a list that may include a form from recursively calling itself. Each call runs `cons` which flattens the retrieved list from an inner recursive call into its own created list of the same level. 

## P13
Function `MAPCAR` maps a list and involves applying a function to its arguments; the final result contains the results returned by the function on each argument. `#'` is a special operator short-hand abbreviation for a function, hence `#'length` is treated as a function and is applied to each argument in the list.

## P14
Same logic as P13 but uses the macro `LAMBDA` or anonymous function instead, which executes each form and constructs a list from the results of the anonymous function.

## P15
Macro `LAMBDA` provides a shorthand notation for a function special form involving a lambda expression; basically an anonymous function builder that returns a function object, and executes at compile time by running the expanded code. 

## P16
Special operator `LET` creates new variable bindings and executes those bindings in parallel; it computes its values using only from its existing environment, where it remains unaffected to changes to its environment after evaluation. Thus, when `f` was called, it uses `factor 2` instead of the later `factor 10` since `f`'s environment only saw `factor 2` on its evaluation.
