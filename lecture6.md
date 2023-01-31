# Lecture 6

## Parsing
- simpler: regular expression matching
- nondeterministic finite state machine
- To represent context free grammars, requires FSM + stack
- program + recursion

## Parsing Problems
- 0: tokenization (easy : given in HW2, but CPUish)
- 1: recursion in parser (you must trust yourself!)
- 2: disjunction: S->A|B
- 3: concatenation: S->ABC

##
- frag: [ACGT]*
- acc: frag -> frag option
- f: match, unmatched suffix s, argument of acc
- matcher: frag -> acc -> frac option
- (fun f -> if f = [] then Some f else None)
- (fun f -> None)
- (fun f -> Some f)

```ocaml
let mnuc nt f a = match f with
    | [] -> None
    | h::t -> if h = nt then Some t else None)
```

## Or P1, P2
```ocaml
let mor p1 p2 = 
    let m1 = mm p1 in
    let m2 = mm p2 in
    (fun f a -> match m1 f a with
    | None -> m2 f a
    | x -> x)
```

## Concatenation
```ocaml
let mam p1 p2 = 
    let m1 = mm p1 in 
    let m2 = mm p2 in
        (fun f a -> m1 f (fun f1 -> m2 f1 a))
```

## Translation environments
- Classic Unix/Linux
- source code `int main (int argc, char** argv) {return argv [1][0];}`
- token INT ID ( INT ID, CHAR * * ID ) ...
- parse - parse tree
- checking typos scope
- intermediate code generation
- asm generation
- as (foo.s -> foo.o)
- ld (foo.o -> a.out)
- kernel => ram

## IDE (Integrate Development Environment)
- Smalltalk
- Xerox PARC
- 1970s
- Smalltalk d.e. written in smalltalk
- image = all your code

## Compilers vs interpreters
- compilers have better runtime performance, security through obscurity
- interpreters keep source around (or something close to it) => easy to debug
  - translation to bytecodes - asm to execute bytecodes
- Java: (JVM)
- Foo.java
- Foo.class (bytecodes)
- Java interpreter java bytecode compiler
- JIT (Just In Time compiler)