Math.NET Symbolics
==================

Math.NET Symbolics is a basic opensource **computer algebra library for .Net, Silverlight and Mono** written entirely in F#.

This project does *not* aim to become a full computer algebra system. If you need such a system, have a look at Axiom or Maxima instead, or for proprietary commercial solutions Maple, Mathematica or Wolfram Alpha.

Some code examples and, after the arrow, the resulting expression as formatted with `Text.format`:

* `(3Q + 2)*4/6` --> `10/3`.
* `(a/b/(c*a))*(c*d/a)/d` --> `a^(-1)*b^(-1)`
* `(a+b)/(b+a)**2` --> `(a + b)^(-1)`
* `Algebraic.expand ((a+b)**3)` --> `a^3 + 3*a^2*b + 3*a*b^2 + b^3`
* `Exponential.expand (exp(2*x+y))` --> `exp(x)^2*exp(y)`
* `Exponential.contract (exp(x)*(exp(x) + exp(y)))` -- > `exp(2*x) + exp(x + y)`
* `Exponential.simplify (1/(exp(x)*(exp(y)+exp(-x))) - (exp(x+y)-1)/((exp(x+y))**2-1))` --> `0`
* `Trigonometric.expand (sin(2*x))` --> `2*sin(x)*cos(x)`
* `Trigonometric.contract (sin(x)**2*cos(x)**2)` --> `1/8 + (-1/8)*cos(4*x)`
* `Trigonometric.simplify ((cos(x)+sin(x))**4 + (cos(x)-sin(x))**4 + cos(4*x) - 3)` --> `0`
* `Polynomial.polynomialDivision x (x**3 - 2*x**2 - 4) (x-3)` --> `(3 + x + x^2, 5)`
* `Polynomial.polynomialExpansion x y (x**5 + 11*x**4 + 51*x**3 + 124*x**2 + 159*x + 86) (x**2 + 4*x + 5)` --> `1 + x + (2 + x)*y + (3 + x)*y^2`
* `Polynomial.gcd x (x**7 - 4*x**5 - x**2 + 4) (x**5 - 4*x**3 - x**2 + 4)` --> `4 + (-4)*x + (-1)*x^2 + x^3`
* `Rational.rationalize (1+1/(1+1/x))` --> `(1 + x)^(-1)*(1 + 2*x)`
* `Rational.simplify x ((x**2-1)/(x+1))` --> `(-1) + x`

```
let taylor (k:int) symbol x a =
    let rec impl n nf acc dxn =
        if n = k then acc else
        impl (n+1) (nf*(n+1)) (acc + (dxn |> Structure.substitute symbol a)/nf*(symbol-a)**n) (Calculus.differentiate symbol dxn)
    impl 0 1 zero x |> Algebraic.expand

taylor 3 x (1/(1-x)) 0Q       --> 1 + x + x^2
taylor 3 x (1/x) 1Q           --> 3 + (-3)*x + x^2
taylor 3 x (ln(x)) 1Q         --> -3/2 + 2*x + (-1/2)*x^2
taylor 4 x (ln(x)) 1Q         --> -11/6 + 3*x + (-3/2)*x^2 + (1/3)*x^3
taylor 4 x (sin(x)+cos(x)) 0Q --> 1 + x + (-1/2)*x^2 + (-1/6)*x^3
```

### Literature

* Computer Algebra and Symbolic Computation - Elementary Algorithms, Joel. S. Cohen
* Computer Algebra and Symbolic Computation - Mathematical Methods, Joel. S. Cohen
* Modern Computer Algebra, Second Edition, Joachim von zur Gathen, Jürgen Gerhard
* Symbolic Integration I - Transcendental Functions, Second Edition, Manuel Bronstein
* Concrete Mathematics, Second Edition, Graham, Knuth, Patashnik
* ... and of course the fundamental theory by Euclid, Newton, Gauss, Fermat and Hilbert.

### Project

Maintained by [Christoph Rüegg](http://christoph.ruegg.name/) and part of the [Math.NET initiative](http://www.mathdotnet.com) (see also [Math.NET Numerics](http://numerics.mathdotnet.com)). It is covered under the terms of the [MIT/X11](http://mathnetnumerics.codeplex.com/license) open source license. See also the [license](LICENSE.md) file in the root folder. **We accept contributions!**

* [@MathDotNet](http://twitter.com/MathDotNet)
* [Ohloh](https://www.ohloh.net/p/mathnet-symbolics)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/mathdotnet)