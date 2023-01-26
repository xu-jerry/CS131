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