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