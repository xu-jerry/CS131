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