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

## P03
`NIL` is a symbol that represents an empty list, false, and the null type. 

## P04
`t` is a symbol that represents the truth boolean value.  

## P05
`SYMBOLP` returns a generalized boolean, `true` if object is of type symbol; `false` if otherwise. `NIL` is a symbol, therefore `SYMBOLP` returns true or in this case `t`

## P06
Returns the  first argument of a `cons`. The list is empty, therefore returns the `nil` symbol.

## P07
A function that creates a new `cons` object. Flattens sub-lists into the new generated list.

## P08
Special-operator `IF` evaluates the expression: selects the `then-form` if true; otherwise `else-form` is selected. Whichever selected form is evaluated and returned. 

## P09
Replace this line with the rule behind this case's four fields.

## P10
Replace this line with the rule behind this case's four fields.

## P11
Replace this line with the rule behind this case's four fields.

## P12
Replace this line with the rule behind this case's four fields.

## P13
Replace this line with the rule behind this case's four fields.

## P14
Replace this line with the rule behind this case's four fields.

## P15
Replace this line with the rule behind this case's four fields.

## P16
Replace this line with the rule behind this case's four fields.
