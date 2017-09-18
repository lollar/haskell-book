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

