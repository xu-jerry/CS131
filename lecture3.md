# Lecture 3
- currying
- recursion
- pattern matching
- type checking
- grammars

## Currying
- use higher order functions so that each function will take in one argument
- Haskell Curry
- let ispos = (<) 0;;
- let isneg = (<) x 0;;
- let isneg x = x < 0;;
- let isneg x = fun x -> (<) x 0;;
- above is lamda expression, aka nameless function
- "syntactic sugar"
- let cons a b = a::b;;

## Recursion
- Why?
  - A lot of problems easily via recursion, not via loops
  - e.g. grammars: specs for parse trees

## Aside on pattern matching
```ocaml
match E with
|P_1 -> E_1
|P_2 -> E_2;;
```
- example:

```ocaml
match n+3 with
|0 -> 57
|x -> x+5
```
|patterns | match|
|--------|-------|
|constant|itself|
|identifier|anything; back to that value|
|P, Q| 2-tuple such that P matches 1st, Q matches 2nd|
|_|anything, but no binding|
- e.g.
```ocaml
match f x with
a, b -> a + b
```

## Recursive Programming
```ocaml
let rec last = fun l ->
    match l with
        |[x] -> x
        |_::b -> last (b)
        |[] -> 0
```
- if remove last line, changes into a partial function
- don't write partial functions!
- How to solve returning anything?
```ocaml
let rec lastd = fun def -> fun l ->
    match l with
        |[x] -> x
        |_::b -> last def (b)
        |[] -> def

lastd -1 li
lastd [] lli
```
- unsatisfactory, since relies on special value
```ocaml
let last = lastd []
```

```
type 'a option = 
    | None
    | Some of 'a
```
discriminant union type
- C/C++ unions either one
- Constructors None Some
```ocaml
match x with
| None -> 0
| Some (n::) -> n
| _ -> 1
```

```ocaml
let rec lasto = fun l ->
    match l with
        |[x] -> Some x
        |_::b -> last (b)
        |[] -> None
```
```
val lasto 'a list -> 'a option
```
with syntactic sugar:
```ocaml
let rec lastd def l =
    match l with
        |[x] -> x
        |_::b -> lastd def (b)
        |[] -> def
```
```ocaml
let rec lastd def = function
    |[x] -> x
    |_::b -> lastd def (b)
    |[] -> def
```

```ocaml
let rec reverse = function
    | [] -> []
    | a::d -> (reverse d) @ a
reverse : 'a list list -> 'a list = <fun>
```
```ocaml
let rec reverse = function
    | [] -> []
    | a::d -> (reverse d) @ [a]
reverse : 'a list list -> 'a list = <fun>
```
## Accumulators in recursive functions
```ocaml
let rec arev a = function
    | [] -> a
    | h::t -> arev (h::a) t

let reverse = arev []
```
## Grammars
- specify syntax
- form of a language
- Simpler idea: regular expressions
- language = set of strings