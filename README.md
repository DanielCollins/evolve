## Genetic Programming Experiments

This is a scheme program implementing [Genetic programming](http://github.com).

You define some test data to train on, giving the correct output for each of a
list of inputs, and the machine attempts to find ("evolve") a program which can
reproduce those results.

### Run it

No unusual features are used, so it should be easy to port to any scheme, but
it was tested using [chicken](https://www.call-cc.org/). If chicken is installed
the easiest way to run evolution is:

    csi src/gp.scm

### Output

You will see something like this:

    generation number 0
    best current specimen: 0
    with error: 6.33361124055445e+16

    generation number 1
    best current specimen: 10000002
    with error: 5.91017846753458e+16

    generation number 2
    best current specimen: 10000002
    with error: 5.91017846753458e+16

    generation number 3
    best current specimen: 10000002
    with error: 5.91017846753458e+16

    generation number 4
    best current specimen: 10000002
    with error: 5.91017846753458e+16

    generation number 5
    best current specimen: (* (+ 1 (* y 6)) (+ 1 (* y 6)))
    with error: 4.63284294645665e+16

    generation number 6
    best current specimen: (* (+ 1 (* y 6)) (+ 1 (* y 6)))
    with error: 4.63284294645665e+16

    generation number 7
    best current specimen: (div (- (+ 11 (* (* (+ (div 2 x) 2) (div 2 (div 2 x))) x)) (* 1000000 (* x (div 2 (div 2 (- 1 x)))))) (+ 1 (* y 6)))
    with error: 2.001225881991e+16

It is printing, after every evolution time step, the best program that evolved
so far, and, the (user defineable) error level of that program.

### Defining the problem to train on

To feed the machine test data, you have to edit the definition of procedure
`rerror`. It receives a sample program as an argument. It can invoke the
sample on arguments using `(run-specimen sample '(x y) a b)` where a and b
are two input arguments. Compare the result with the correct output, and return
any kind of error or value, which the machine will try to minimise.


### Is it any good?

No.

It's a good example of how easy lisp makes symbolic program, and it's also very
fun to watch it working, but it is not a particularly practical machine
learning system.

Genetic programming systems in general no longer seem to be popular, (perhaps
for good reason?), and mine in particular suffers firstly from a weak
(non-turing-complete) program language, and secondly from slow inference.
Both of those problems could be somewhat mitigated with more work.

One thing it is decent at currently is quickly finding the general shape or
"order" of polynomial or exponential expressions, but it struggles with the
apperently much easier problem of finding an exact constant expression.
