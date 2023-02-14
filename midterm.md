# Lecture 1

Quiz: Write a program that take input a string and output, in descending order, the number of times a word occurs. For example:

Input:\
Now is the time for a 10-minute quiz time now a for a quiz.

Output:\
3 a\
2 quiz\
2 for\
2 time\
1 Now\
1 now\
1 the\
1 minute

## DE Knuth
- wrote books for Programming Languages
- side project: invented program Tex for typesetting text
  - written in Pascal
- published some ideas he came up with while writing Tex
- also published documentation
- side project to side project: wrote a book called The Tex Book, in Tex\
- `texbook.tex --> beautiful book via tex`
- new idea: wrote documentation in same file as code
- wrote paper on Literate Programming in CACM
- `litprog.texpas` can generate `litprog.pas`, `litprog.exe`
- it can also generate `litprog.tex` and the CACM paper
- M. D. McIlroy, contributed to Unix and Posix
  - added pipes "|"
- hash trie for the quiz
- afterword by McIlroy said he would use shell scripts and hook them together using pipes
  - e.g. tr breaks into words, changes all non-alphabetic characters to newlines
  - `tr -cs 'A-Za-z' [ln*]`
  - complement, squeeze
  - `sort`
  - `uniq -c`
  - count duplicates
  - `sort -nr`
  - numeric, reverse
  - In total, `tr -cs 'A-Za-z' [ln*] | sort | uniq -c | sort -nr` 

## Notation
- This class is basically a class on CS Notation
- Math, Chemistry, etc. do not have classes on notation- why?

## Sapir-Whorf Hypothesis
- The structural diversity of languages is essentially limitless
- The language that we use, to some extent, determines how we think
- e.g. Inuits have 7 words for snow (not true)
- e.g. Chinese numbers are shorter to say, so people who speak Chinese are better at math.
- first part of the hypothesis is true, second part is false
- true for programming languages?

## Logistics
- Read 1-3, 5, 7, 9
- syntax + OCaml
- Eggert Late Policy
- Assignments due 11:55PM

## Topics
Theory
- Syntax
- semantics
- functions
- names
- types
- control
- objects
- exceptions
- concurrency
- scripting
- metaprogramming

Practice
- Ocaml
- Prolog
- Java
- Scheme
- Python

## Judging Languages
- what makes for a good language in practice?
- costs: maintenance of program
- efficiency at runtime (CPU time / memory)
- training / community / documentation
- portability
- development time
- testability
- scalability
- compile times
- runtimes
- security

## Language Design Issues
- Orthogonality
- C++/C cannot return arrays or functions, only pointers to them

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
- functional form / higher order function: function whose domain is a function
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
  - O(1)
- Lisp: cons car cdr
  - cons ::
  - car hd
  - cdr tl
- let car a::b = a
  - syntax error
- don't try to take the head of a list
- let cons(a, b) = a::b;;
- val cons : 'a * 'a list -> 'a list = <fun>
- let cons a b = a::b;;
- val cons : 'a -> 'a list -> 'a list = <fun>

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

# Lecture 4

## Syntax
- definition: form of language independent of meaning
- formal spec for syntax is written in a quasi-programming language
- Natural language syntax examples
  - "Colorless green ideas sleep furiously." - N. Chomsky
  - syntax correct, but meaning incorrect
  - "Ireland has leprechauns galore." - P. Eggert
  - galore is adjective
  - "Time flies."
  - can be noun verb or verb noun - ambiguity

## "Good" vs "Bad" Syntax
- inertia - people already used to it
- simplicity, regularity (e.g. OCaml)
- readability
- writeability (e.g. APL, a programming language: +/$\iota$ 100)
- it's unambiguous
- it's redundant
- e.g. no closing parentheses before semicolon: b*(c+d); vs b*(c+d;
- maintanability
- Leibnitz's criterion
  - "Form of a proposition should mirror reality."
  - if (i >= 0 && i < N)
  - if (0 <= i && i < N)

## Tokens vs Lexemes
- integer - 23, 0x1234
- float - 23e-19
- identifier - abc0, _abc_
- if - if, i\ (new line) f
- else - else
- Tokens - what grammars are built from
- Lexemes - sequence of chars represent one of a class of tokens

## Token issues
- byte sequence -> character sequence
- UTF-8 Unicode Transform Format
- each char is a sequence of 8-bit bytes (not every byte sequence is valid)
- debugging is hard
- non-tokens:
  - comments
  - whitespace
- tokenizers are greedy
```c++
print("w");
// What the *@!! is &@??/
print("x");
print("y");
```
- trigraphs

## Grammar
- compact notation that specifies a language syntax
- language: set of strings
- string: finite sequence of tokens
- token: member of finite set of your choice
- $\{a^nb^nc^n | n>2\}$
- tokens: {"aabbcc"}

## Context-Free Grammars
- finite set of tokens (terminals)
- finite set of nonterminals
- start symbol (a nonterminal)
- finite side of rules, each
  - nonterminal lhs -> finite sequence of symbols rhs

## Internet RFC (Requests for comment) 5322
- for email, specifies a grammar for email headers
- Message-ID: <eggert.$xyz."abc"@cs.ucla.edu>
- BNF (Backus Naur Form)
- msdg-id = "<" dot-atom-text "@" id-right ">"
- id-right = dot-atom-text / no-fold-literal
  - vs id-right = dot-atom-text
  - id-right = no-fold-literal
- no-fold-literal = "[" *dtext "]"
- dot-atom-text = 1\*atext \*("." 1\*atext)
  - atex1 = atex
  - atex1 = atex1 atex
  - trail = 
  - trail = trail "." atext1
  - dot-atom-text = atex1 trail
- atext = ALPHA / DIGIT / "!" / "#" / "$" ...
- !#$%&'*+-/=?^_`{}|~
- dtext = %d33-90 / %d94-126
- ascii character between 33-90 and 94-126 (most printable ones)

## ISO Standard for EBNF
- "x" 'x' are both valid for strings
- [ option ]
- { repeat0+ }
- ( grouping )
- infix ops
- A-B, A except B
- A,B, A followed by B
- A|B, A or B
- lhs = rhs
- syntax = syntax rule, {syntax rule};
- syntax rule = meta id, '=', defns list, ';';
- defns list = defn, {'|', defn};

# Lecture 5

## Grammars
- notations (one more)
- trouble
- programs that deal c grammar
- BNF notations
- EBNF notation
- syntax charts diagram
- racetrack

## Grammar for a bit of Scheme
- \<cond\> -> (cond \<cond clause\> +)
- | (cond \<cond clause\> * (else \<sequence\>))
```
def parse_cond():
    eat("(")
    eat("rand")
    if next_two_syms(["(", "else"]):
        eat("("); eat("else"); parse_sequence(); eat(")");
    else;
```

## What can go wrong in a grammar?
1. Use a nonterminal, but don't define it on LHS
2. define a nonterminal, but don't use it
3. You try to do too much with the grammar
4. Ambiguous grammars
   
- S->S or S->T and T->S

- S-> NP VP
- NP -> N
- NP -> Adj NP
- VP -> V
- VP -> VP Adv
- Adj -> blue | green | angry
- Adv -> slowly | quickly | anxiously
- N -> dog | dogs | cat | cats
- V -> bark | barks | meow | meows
- now, too generous because number doesn't have to agree

## C grammar
stmt: \
>   ; \
    return expr$_{opt}$; \
    continue; \
    break; \
    goto ID; \
    expr; \
    while ( expr ) stmt \
    {stmt-list$_{opt}$} \
    for ( expr$_{opt}$ ; expr$_{opt}$; expr$_{opt}$ ) stmt \
    do stmt while (expr); \
    if (expr) stmt \
    if (expr) stmt else stmt \
    switch (expr) stmt 

- require parentheses around expr bc of code such as `while p * q`
- dangling else is ambiguous

stmt: \
> stmt$_1$ \
> if (expr) stmt

stmt$_1$: \
>   ; \
    return expr$_{opt}$; \
    continue; \
    break; \
    goto ID; \
    expr; \
    while ( expr ) stmt \
    {stmt-list$_{opt}$} \
    for ( expr$_{opt}$ ; expr$_{opt}$; expr$_{opt}$ ) stmt \
    do stmt while (expr); \
    if (expr) stmt else stmt \
    switch (expr) stmt 

for most practice programming languages, 3 kinds of ambiguity
- ambiguity
- associativity
- dangling 'else', etc. (ocaml has match expressions)
- abstract syntax + parse tree vs concrete syntax + parse tree

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

# Lecture 7

### For next week:
- read all Java chapters

## Types
- Sets
- ways to interpret data
- properties of data
- set of things you know about a value in your program at compile-time
- interfaces to data
- set + operation

## Two type ideas
- abstract (you know type's name + ops)
  - better for modularity
- concrete (you know how type is implemented)
  - better for performance

## Float (32-bit floating point #s)
- C std is silent about float details
- 99.99% of compilers
- 1 8 23 bits for sign, exponent, and fraction
- $\pm2^{e-127}\cdot1.f_2$
- 0<e<255
- if $e = 0$, $\pm2^{e-126}\cdot0.f_2$
  - tiny numbers (include +0 -0)
- if $e=255, f=0$ $\pm\infty$
- if $e=255, f\neq 0$ $\pm NaN(f)$
- v = 1e300 * 1e300
- w = 1/v -> 0.0
- x = -v -> $-\infty$
- y = 1/x -> -0.0
- n = 0.0/0.0 -> NaN
- also $\infty - \infty$, $\infty \cdot 0$
- $(a=b) \iff (a-b=0)$
- tiny numbers allow if you subtract two numbers, you will never get 0 if they are not equal

## Uses of types
- annotations of programs
  - easier to read
  - compiler can take advantage
  - pid_t p = fork();
- inference
- checking
  - static
  - dynamic
  - strongly typed

## Polymorphism
- a function with multiple types is polymorphic
- print(sin(x))
- machine code: sin\$f and sin\$d
- overloading: can be implemented via name mangling
- coercion: 
  - float f = ___
  - double g = sin(f);

## Parametric polymorphism
- ad hoc vs universal polymorphism
- a function's type contains type variables (parameters)
- List\<int\> List<T>
- int list 'a list

c is a collection
```java
for (Iterator i = c.iterator(); i.hasNext();) 
    if (i.next().length == 1)
        i.remove()
```

To fix:

(old Java)
```java
for (Iterator i = c.iterator(); i.hasNext();) 
    if ((string) i.next().length == 1)
        i.remove()
```
New java
```java
for (Iterator<String> i = c.iterator(); i.hasNext();) 
    if (i.next().length == 1)
        i.remove()
```

## Two forms of polymorphic types
1. Templates
   - ```
     define template for List<T> {
        char a[sizeof(T)]
     }
     ```
   - Then instantiate it with List\<String\> 
2. Generics
   - define a generic type List\<T\> {
     }
- similar in syntax, but templates get compiled separately and can be optimized
- generics a little slower, can't have sizeof operator evaluated at compile time
  - rely on the fact all types smell the same

## Java's 2 types
- primitive types
  - int, char, bool, float, double
- reference types
  - Object, String, ...
  - internally represented by pointers
- generics do not work with primitive types, only reference types
- Object -> (List -> ArrayList), String, Thread
```java
List<String> ls = ...;
List<Object> lo = ls; // this line is wrong
lo.add(new Thread());
String s = ls.get();
```

## Subtypes
- Thread is a subtype of Object
- const char * vs char *
- char *cp
- char const *ccp
```cpp
ccp = "abc";
cp = ccp; // no good
ccp = cp; // ok
cp[1] = 'y' // would yell at us
```

# Lecture 8
```java
void printall (Collection<?> c) {
    for (Object a:c) {
        System.out.println(a);
    }
}

Collection<String> cs = 
printall(cs);
```
- aside: `Collection<Integer>`
- wrapper class for int

## Wildcards
- similar to 'a in Ocaml
- bounded wildcards: `<? extends Shape>`
- `Collection<?> = Collection<? extends Object> != Collection <Object>`
```java
void <S, T>convert (T [] a, Collection <S super T> c) {
    for (T o: a)
        c.add(o);
}

String [] as = ...;
Collection<Object> co = ...;
convert(as, co)
```
- known as bounded wildcards
```java
void <T>convert (T [] a, Collection <? super T> c) {
    for (T o: a)
        c.add(o);
}

String [] as = ...;
Collection<Object> co = ...;
convert(as, co)
```

## Type casting and Erasure
```
Object o...
String s = (String) o
Collection<String> cs = ...;
```
- runtime just gets simple summary of type
- (Collection<string>) o <-- illegal!

## Duck Typing
-  if it waddles & quacks, it's a duck
```python
o = ...
try: 
    o.waddle()
    o.quack()
except:
    print("not a duck! ouch!")
```

## Names & Bindings
- identifier and relationship between name & its value
- values: int i = 27;   
  - value is 27
  - value is address of the int in memory
  - value is # bytes in i's representation
- binding time: moment when binding occurs
  - 1. during runtime (e.g. assignment, can be repeated)
  - 2. at block entry
  - 3. at link time
```java
int j(int j) {
    int j;
    struct j{int j;}x;

    # include<j>
    # define j j
    j: goto j;
}
```
- ad hoc namespaces
- labeled namespaces:
  - ```
    n = {'a':1, 'b':27}
    n.a
    ```

## Information Hiding
- module
- implementation
- a, bc, ..., 2
- want to supply interface- c and q public
- two ways:
  - (Java):
    - public - visible to any code that sees the class
    - private - visible only to class
    - [default] - visible to any class in same package
    - protected - also visible to subclasses
  - (OCaml)
    - Signature = API for a class
    - compile-time ops on signatures
    - bigsig{a() b() c() d()}, smallsig{a() c()}

## Java - like C++
- IoT (Internet of Things), 1994ish, toasters on the Internet
- C++:
  - crashes too much
  - updates took too long
  - recompile for each platform (ARM, x86-64, RISC-V, ...)
- Sun - went to XeroxPARC, Smalltalk (bytecoded interpreter & runtime checking)
- Merged C++ and Smalltalk, ~~Oak~~, Java
- built a browser in Java + extensions in bytecodes, Mosaic -> Mozilla Firefox
- multithreaded apps
- $\Delta$ from C++
  - primitive types: int long short have well defined widths
  - left-to-right evaluation
  - null dereferences and subscript errors cause exceptions instead of undefined behavior
- Classes are single inheritance
- can implement many interfaces
- inheritance is like money, interfaces is like debt

## Abstract classes & methods
```java
abstract class C1 extends P {
    abstract int m();
    int n() {return f(x)}
}
```

## Final methods
```java
class C extends P {
    final int m() {
        return ...
    }
}
class D extends C {
    int n() {}
}
```
- cannot be overwritten
- for not trusting children
- performance benefit, can generate more efficient code because no possibility of overwriting

## SMP (Symmetric multiprocessing)
- Many CPUs, one RAM
- Thread's life cycle
- ```java
  t = new Thread(...); // State: NEW
  t.start(); // RUNNABLE
  do IO // BLOCKED
  wait timer // TIMEDWAITING
  rendezvous // WAITING
  exit // TERMINATED
  yield // RUNNABLE
  ```