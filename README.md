<!--
Welcome to your new proposal repository. This document will serve as the introduction and 
 strawman for your proposal.

The repository is broken down into the following layout:

  /README.md        # intro/strawman (this file)
  /LICENSE          # ECMA compatible license (BSD-3 Clause)
  /src              # ecmarkup sources for the specification
  /docs             # ecmarkup output

To build the specification, run:

  npm run compile

To preview the specification, run:

  npm run start

It is recommended that you configure GitHub Pages in your GitHub repository to point to the
'/docs' directory after you push these changes to 'master'. That way the specification text
will be updated automatically when you publish.

-->

# Proposal to add functional operators to ECMAScript

This strawman seeks to define the possible syntax and semantics for functional operators
for ECMAScript. 

## Status

**Stage:** 0  
**Champion:** _None identified_

_For more information see the [TC39 proposal process](https://tc39.github.io/process-document/)._

<!-- The following sections are optional and may be uncommented if needed: --->

<!-- # Motivations -->
<!-- Motivations and use cases for the proposal --->

# Proposal

A "functional operator" is an operator-like sigil that acts like a function at runtime. In 
addition, a "binary functional operator" allows either the first or second operand to be fixed.

Most functional operators are written as `{<<op>>}` where `<<op>>` is one of the binary or
unary operator punctuators, or one of the `instanceof`, `in`, or `typeof` keywords. In cases
where an operator has an overloaded definition between both binary and unary forms, the unary
versions of the operator have the form `{~<<op>>}`.

Each functional operator can be expressed as existing JavaScript given the following syntactic
conversions:

```js
// exponentiation operator function
{**}                // (a, b) => a ** b

// multiplicative operator function
{*}                 // (a, b) => a * b
{/}                 // (a, b) => a / b
{%}                 // (a, b) => a % b

// additive operator function
{+}                 // (a, b) => a + b
{-}                 // (a, b) => a - b

// shift operator function
{<<}                // (a, b) => a << b
{>>}                // (a, b) => a >> b
{>>>}               // (a, b) => a >>> b

// relational operator function
{<}                 // (a, b) => a < b
{<=}                // (a, b) => a <= b
{>}                 // (a, b) => a > b
{>=}                // (a, b) => a >= b
{instanceof}        // (a, b) => a instanceof b
{in}                // (a, b) => a in b

// equality operator function
{==}                // (a, b) => a == b
{===}               // (a, b) => a === b
{!=}                // (a, b) => a != b
{!==}               // (a, b) => a !== b

// bitwise operator function
{&}                 // (a, b) => a & b
{|}                 // (a, b) => a | b
{^}                 // (a, b) => a ^ b

// logical operator function
{&&}                // (a, b) => a && b
{||}                // (a, b) => a || b

// unary additive operator function
{~+}                // (a) => +a
{~-}                // (a) => -a

// unary bitwise operator function
{~}                 // (a) => ~a

// unary logical operator function
{!}                 // (a) => !a

// other unary operator function
(typeof)            // (a) => typeof a
```

Each functional operator is a frozen function that exists at most once per realm. This can help to 
cut down on the number of function objects allocated within a given program.

## Fixed arguments

In addition, binary functional operators may fix either the first or second operand:

```js
// fixed arguments
{+} 1               // (a) => a + 1

2 {*}               // (a) => 2 * a
```

In these cases, the function returned is a unique frozen function object.

# Examples

```js
const sum = ar.reduce({+});

const result = numbers 
  .map({*} 2)  // scale
  .map({+} 5)  // offset

const strings = numbers
  .map({+} "");

const numbers = strings
  .map({~+});

const positive = numbers
  .filter({>} 0);

const halves = numbers
  .map({/} 2); // no need for regexp lookahead/cover grammar
```

<!-- # Grammar -->
<!-- Grammar for the proposal. Please use grammarkdown (github.com/rbuckton/grammarkdown#readme) syntax in fenced code blocks. -->

<!-- # Semantics -->
<!-- Static and runtime semantics of the proposal -->

<!-- # References -->
<!-- Links to other specifications, prior art, etc. -->

# Prior Art

* [F#](http://fsharp.org) symbolic operators.