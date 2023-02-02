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