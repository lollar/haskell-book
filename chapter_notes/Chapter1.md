### Chapter 1
# All You Need is Lambda
### 1.1 All You Need is Lambda
Lambda calculus is one process for formalizing a method.
### 1.2 What is functional programming?
- Programs are a combination of expressions
- Purity is sometimes used to mean referential transparency
  - Referential transparency means that hte same function given the same values to evlaute, will always return the same result
### 1.3 What is a function?
[EXAMPLE 1](https://github.com/lollar/haskell-book/examples/example1)
The important part of how these relations are defined is that the return value will never change given the same input
[EXAMPLE 2](https://github.com/lollar/haskell-book/examples/example2)
In contrast, example 2 is not a valid function.
### 1.4 The structure of lambda terms
Three basic components:
- expressions
- variables
- abstractions

The word expression refers to a super set of all those things.

An abstraction is a function consisting of two parts: the head, and the body.
The head contains the lambda and a variable. The body is the expression returns when applied.

### 1.5 Beta reduction
When applying a function to an argument:
  - substite the input expression for all instances of bound variables within the body of the abstraction
  - eliminate the head of the abstraction

### 1.6 Multiple arguments
- Each lambda can only bind one parameter and can only accept one argument.
  - Functions that require multiple arguments have multiple, nested heads.
  - This is the concept commonly known as `currying`
  - convenient shorthand for two nested lambdas: `$xy.xy`

### EXAMPLES
#### Identity Function
```
$x.x
($x.x)1
[x := 1]
1
```
#### Multiple Argument Lambda
```
$xy.xy
($xy.xy)1 2
($x.($y.xy)) 1 2
[x := 1]
($y.1y) 2
[y := 2]
1 2
```
#### Mutliple Argument Lambda
```
$xy.xy
($xy.xy)($z.a) 1
($x.($y.xy))($z.a) 1
[x := ($z.a)]
($y.($z.a)y) 1
[y := 1]
($z.a) 1 --| We can still apply this one more time.
[z := 1] --| But there is no z in the body of the function, so there is nowhere to put a 1. We elminate the head, and the final reasult is
a
```
#### Continued reduction example
```
($xyz.xz(yz))($mn.m)($p.p)
($x.$y.$z.xz(yz))($m.$n.m)($p.p) --| nothing reduced just made currying explicit
($y.$z.($m.$n.m)z(yz))($p.p) --| apply outer most lambda, which was binding x, to the first argument `($m.$n.m)`
$z.($m.$n.m)(z)(($p.p)z) --| We applied the y and replaced the single occurnce of y with th enext argument `$p.p`
--| At this point z is irreducible because there is no argument to apply. We have to go inside each term one layer at a time until we find something reducible.
$z.($n.z)(($p.p)z) --| Apply lambda binding m to the argument z. 
$z.z
```
#### Equivalence Exercise Answers:
1. B
2. C
3. B

### 1.7 Evaluation is simplification
- Normal form refers to `beta normal form`
  -  Beta normal form is when you cannot reduce terms any further

### 1.8 Combinators
- A combinator is a lambda term with no free variables
- Server only to `combine` the arguments they are given
- The following are examples of combinators because every term in the body occurs in the head:
1. `$x.x` --| x is the only varable and is bound because it iis bound by enclosing the lambda
2. `$xy.x`
3. `$xyz.xz(yz)`
- The follwoing are not because there's one or more free variables:
1. `$y.x` --| Here y is bound but x is free
2. `$x.xz` --| z is free

### 1.9 Divergence

Not all reducible lambda terms to a beta normal form, sometimes they diverge.

Divergence means that the reduction process never ends.

#### Omega that diverges
1. ($x.xx)($x.xx)
x in the first lambda's head becomes the second lambda.

2. ([x := ($x.xx)|xx)
Using [var := expr] to denote what x has been bad to.

3. ($x.xx)($x.xx)
Substituting ($x.xx) for each occurence of x. We're back to where we started and this reduction process never ends - we can say omega diverges.

This matters because terms that diverge don't produce an answer or meaningful result.

