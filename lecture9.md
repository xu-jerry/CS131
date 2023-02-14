# Lecture 9

## For next time
- read Webber on Prolog (3 chapters)

## Object
- Thread subclass
- String subclass
- Class subclass
- JDK dec: Class Object
- ```java
  public class Object {
    public Object();
    int hashCode();
    boolean equals(Object obj);
    String toString();
    final Class<? extends X> getClass();
    protected Object clone()
        throws CloneNotSupportedException;
    DEPRECATED protected void finalize()
        throws Throwable;
    wait()
    notify()
    notifyAll()
  }
  ```
- ```java
  a[a.length - 1] = new Object();
  for (i = 0; i < a.length; i++) {
    if (a[i] != p)
        break;
  }
  ```
- ```java
  int h = o.hashCode();
  a[h % a.length]
  o.equals(o1) -> o.hashCode == o1.hashCode();
  ```
- equals should be (like in math) symmetric, reflexive, and transitive
- hashCode should not change if object doesn't change
- ```java
  System.out.println(o)
  o.toString()
  ```
- some defaults - hashCode takes the 32 least significant bits, equals checks memory location equality
- ```java
  o.getClass.toString()
  ```
- reflection: when a program "looks" at itself
- X static type of expression getClass()
- Java has garbage collection:
  - at any time it can reclaim unused objects
  - suppose your class `DBConnection` has a file descriptor
  - ```java
    class DBConnection {
        void finalize {self.close();}
    }
    ```
- creating a Thread:
  - `class MyThread extends Thread {}`
  - ```
    RunnableRectangle {
        class RRect implements Runnable {
            void run() {
                delegation
            }
        }
    }
    ```
  - ```java
    interface Runnable {
        void run();
    }
    RRect o = new RRect();
    new Thread(o);
    ```

## Collisions/races
- synchronized keyword
- A synchronized method
- ```java
  synchronized int m() {
    o.lock();
    // the above and below are added by compiler when you have synchronized keyword
    o.unlock();
  }
  ```
- spin lock

## Blocking Mutexes
```java
o.wait()
o.notify()
o.notifyAll()
```
- wait - remove lock held by this thread. Wait for o to become "available"
- when wakes up (gets notified), regets lock()
- notify - some thread waiting on o
- all

## Semaphore
- create it with a capacity
- s.acquire()
- s.tryAcquire()
- s.release()
- Exchanger x
- a = x.exchange(v)
- b = x.exchange(w)
- CyclicBarrier
- embarrasing parallelism
- CountDownLatch

## Performance + threads
- improve performance by caching values into registers
```java
for (o.i=0; o.i < a.length; a.i++)
    if (o.a[o.i] == p)
        break;
int i = 0;
for (i = 0; i < a.lenght; i++)
    if (o.a[i] == p)
        break;
    o.i = i;
```

## Volatile
- disables optimizations to get "understandable" behavior

## Java Memory Model (JMM)
- Minkowski diagrams
- abstract Java machine has threads
- Each thread has sequential semantics that make sense for assignments & allows optimizations via caching (as if) for sequential programs
- 3 classes of operations
  - A. normal load, normal state
  - B. volatile load, enter monitor
  - C. volatile store, exit monitor
- can reorder the ops if sequential says ok

2nd op
| |A | B | C|
|--|--|---|--|
|A|ok|ok|
|B|
|C|ok|

## Constructor + JMM
```java
class Bad {
    Bad() {
        o=self.i // <- invalid, cannot tamper with other threads
        ...
    }
}

static Object o;
print(o.x)
```