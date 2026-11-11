# Environments and the Toy Evaluator

Tracing the following form from E4,

```lisp
(eval-expr '(let ((x 2))
              (let ((f (lambda (y) (+ x y))))
                (let ((x 100))
                  (f 1))))
           '())
```

The lambda branch in `eval-expr` calls `(make-closure (cadr expr) (caddr expr) env)`, which captures the defining environment, `env`. The outer `let` extends the environment with `x = 2`. When the next `let` evaluates the lambda, `make-closure` captures `((x . 2))` and `f` is bound to `(:closure (y) (+ x y) ((x . 2)))`. The final `let` extends the current environment to `((x . 100) (f . closure) (x . 2))`. The body `(f 1)` is called from this extended environment, and it exists only while the body runs.

When `(f 1)` runs, `eval-expr` sends the head `f` through `lookup` and gets the closure back. The argument `1` is evaluated next, and then `apply-closure` takes over. It ignores the caller's environment and extends the saved `((x . 2))` with `y = 1`, so `(+ x y)` returns 3. The `env` that `make-closure` saves is the one `eval-expr` holds when it meets the lambda, not the one a later call site has. Since `extend-env` builds a new list and never modifies the old one, the captured `((x . 2))` is still intact after the later `let` shadows `x`.

If `apply-closure` extended the caller's environment instead, the body would then see the caller's `x = 100`, because `lookup` takes the first match, and the result would be 101. That would make the language dynamically scoped, since a function body would use the bindings of whatever calls it instead of the bindings where the lambda was written.

CLISP is a Lisp-2, so variables and functions live in separate namespaces. A function held in a variable is still a variable, so calling it takes `funcall`. A named function passed as an argument would also need `#'`, which is shorthand for `function` and asks for the function bound to that symbol, as P13 does with `#'length`.

The toy language is a Lisp-1, where one environment holds both. In the application branch of `eval-expr`, the head goes through `eval-expr` like any other expression, so `f` is looked up in that same environment and comes back as a closure. `apply-closure` then runs it, which is why `(f 1)` needs no `funcall`. The language also doesn't need `#'`.

So, the form traced above would need `(funcall f 1)` in the host CLISP, as P16 does with `(funcall f 3)`.
