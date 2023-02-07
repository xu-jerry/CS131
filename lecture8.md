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