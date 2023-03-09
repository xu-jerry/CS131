# Lecture 15

## Garbage collection
- mark+sweep needs help to find roots
  - slots in objects
- (C, C++) G.C.
  - gcc = C++
  - emacs = C

## Conservative G.C.
- stack, assume all roots unless proven otherwise
- depending on location of heap, if high memory addresses, mostly pointers to heap
- apply similar tricks to heap itself
- doubly linked list
  - instead of keeping two pointers, keep one pointer that is the xor of the two pointers
  - to keep track, have to have two pointers
- forces you to follow the specs

## Java G.C.
```c
malloc(32)
```
- want this to be fast
- "generation-based copying collectors"
- hp - heap pointer
- hl - heap limit
- nursery: increments hp
- left is more old
- most pointers go left
- partition objects into generations
- only need to garbage collect the youngest
- takes scattered nursery and create a new nursery
- mark and copy, no sweep phase
  - wasting cache lines on garbage
- use cache, page faults for pointers going other direction6

## C-Python G.C.
- reference counting
- every time, load increment store or load decrement store
- slow, but interpreted
- problem: self pointers, loop
- every once in a while, do mark and sweep
- traditional solution:
  - don't create cyclic data structures
  - make sure to break the cycle before using it
```python
d = {}
e = {}
d[2] = 2
e[5] = d
# when done using:
d[2] = null
```

## Quicklists
- generation-based copying collector
- nursery
- reordering, causes garbage collector slow

## Multithreading
- run the G.C. in a separate thread!
- nursery collisions?
  - give each thread its own nursery
  - as long as no pointer from one nursery to another

## Real time G.C.
- <1ms
- does a bounded bit of G.C.

## OO Languages
- OO style != OO language
- add extra pointers to objects
  - how to call methods
- no such thing as the object oriented style/paradigm
- OO paradigms galore
  - some major differences
    - inheritance vs interfaces
    - classes vs prototypes (like a class, p=o.clone() p.x1(n) p.x2(m))
      - e.g. javascript uses prototypes
    - fully O.O. vs partially O.O.
      - fully: all values are objects
        - Python
        - Ruby
        - cleaner
      - partially: some are objects, some are not
        - C++, Java
        - faster

## Finalizers
- o.finalize()
  - easy to implement in mark+sweep
  - generation-based copying collector (not doable!)
- now deprecated

## Parameter Passing
- efficient + simple (easy to explain) + safe
- hard to do all 3 at once
- call by value: caller evaluates args, passes copies to callee
  - really simple, really safe
  - inefficient: large values
- call by reference
  - caller evaluates addresses of args
  - passes addresses to callee
  - not as simple, not as safe