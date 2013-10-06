# math_expressions #

A math library supporting REAL, INTERVAL and VECTOR evaluations of
mathematical expressions.

It is partly inspired by [mathExpr][] for Java.

**Note:** This library is still in an early state, the test coverage is not
perfect, the performance is not optimized and some features are still
unimplemented. Basic REAL and INTERVAL evaluations should work though.
Suggestions and pull requests are always welcome!

## Features ##

* Parsing, simplification and derivation of mathematical expressions.
* Evaluation of expressions in different modes (Real, Vector, Interval).
* Supporting most basic functions out of the box.
* Well documented.

### What's not working yet? ###

* Evaluations in vector space.
* Composite functions.
* Parser is a little rough.

## Documentation ##

See [DartDoc][dartdoc].

## Examples ##

### 1. Expression creation and evaluation ###

This example shows how to evaluate

![Equation 1][exampleEq1]

for
![xy][exampleEq1xy]

#### Build the expression ####

You can either create an mathematical expression programmatically or parse a string.

* Create the expression programmatically:
```
  Variable x = new Variable('x'), y = new Variable('y');
  Power xSquare = new Power(x, 2);
  Cos yCos = new Cos(y);
  Number three = new Number(3.0);
  Expression exp = (xSquare + yCos) / three;
```

* Create the expression via the parser:
```
  Parser p = new Parser();
  Expression exp = p.parse("(x^2 + cos(y)) / 3");
```

#### Evaluate the expression ####

* Bind variables and evaluate the expression as real number:
```
  // Bind variables:
  ContextModel cm = new ContextModel();
  cm.bindGlobalVariable(x, new Number(2.0));
  cm.bindGlobalVariable(y, new Number(Math.PI));
  
  // Evaluate expression:
  double eval = exp.evaluate(EvaluationType.REAL, cm);

  print(eval) // = 1.0
```

### 2. Expression simplification and derivation ###

This example shows how to simplify and derive

![Example 2][exampleEq2]

* Expressions can be simplified and differentiated with respect to a given variable:
```
  Expression exp = p.parse("x*1 - (-5)");

  print(exp);            // = ((x * 1.0) - -(5.0))
  print(exp.simplify()); // = (x + 5.0)

  Expression expDerived = exp.derive('x');
  
  print(expDerived);            // = (((x * 0.0) + (1.0 * 1.0)) - -(0.0))
  print(expDerived.simplify()); // = 1.0
```

### 3. Interval arithmetics ###

todo

For more code, see [example.dart](example/example.dart).

[mathExpr]: http://www-sfb288.math.tu-berlin.de/~jtem/mathExpr/
[dartdoc]: http://fkleon.github.io/math_expressions/
[exampleEq1]: http://latex.codecogs.com/gif.latex?%28x%5E2%2Bcos%28y%29%29%2F3
[exampleEq1xy]: http://latex.codecogs.com/gif.latex?x%3D2%2Cy%3D%5Cpi
[exampleEq2]: http://latex.codecogs.com/gif.latex?x*1-%28-5%29
