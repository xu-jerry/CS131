# Lecture 2

## Agenda
- what makes a P.L. (programming language) "good"?
- functional programming
- syntax

## What makes a P.L good?
- orthogonality
  - every feature is independent
- efficiency
  - among typical implementations
  - C++ > Java > Python
  - OCaml ~ Java
  - but interpreter is ~ Python, compiled OCaml ~ C++
  - mostly talking about CPU time
  - can also refer to RAM, compile-time, run-time, power / energy, network latency / throughput
- simplicity (learning/doc/implementation)
  - PostScript, e.g. no order of operations because uses stack
- familiar notation
- safety
  - compile-time check vs run-time check vs no (undefined behavior)
- friends / community
- packages / libraries

## Functional Programming
|style                | e.g. | unit of computation | hookups
|---------------------|---|---|---
|imperative           |C++, Python| commands| C<sub>1</sub>; C<sub>2</sub>
|functional           | ML, F#, Scala | function | F(G(x))
|logic                | Prolog | predicate | P & Q, P \| Q
| quantum programming | ? | ? | ?
- give up assignment side effect
- logic programming also gives up functions
- object oriented is another dimension

## MapReduce
- Google C++ systems 1990s-2000s
- each machine runs C++ code, then combine
- functional programming
- independent pieces
- map in parallel, then reduce by combining results of parallel processing

## History of Functional programming
- FORTRAN first successful programming language
- John Backus
- imperative
- 2 big problems
  - hard to parallelize
  - lack of clarity
- Backus - inspired rebellion against von Neumann-style programming

## Function
- math: mapping from a domain to a range
- functional form / higher order function: function hose domain is a function
- f(x) = x^2 vs $\int_0^1f(x)dx$ = $\int(0, 1, f)$
- $f \circ g \equiv f(g(x))$ = $(\circ (f, g))(x)$
- referential transparency

## OCaml
- basic properties
  - compile-time, (static) type checking
  - like C++, Java, unlike Python, Scheme
  - you need not write down the types, typically type inference
  - it manages storage for you (garbage collector) (no free or del)
  - Good support for higher order functions
  - REPL- read evaluation point loop
- ocaml or /usr/local/cs/bin/ocaml
- let x = 3+4*5
- weird error message if 1 < 2 then "a" else 3;;
- [1;3;-7];;
- lists are homogeneous
- (1, "a", false)
- tuple heterogeneous fixed length
- empty list is 'a list = []
- unit type is empty tuple
- functions only take in 1 argument (can be list or tuple)
- :: is a function with type:
- 'a -> ('a list -> 'a list)
- list constructor
  - 3::[4;9] => [3;4;9]