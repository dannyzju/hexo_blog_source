---
title: 'Java Multithreading: Run Two Synchronized Methods Concurrently'
date: 2017-05-17 09:57:05
tags:
- tech
- Java Multithread
---

## I. Question
If i synchronized two methods on the same class, can they run simultaneously on the same object? for example:
```java
class A {
    public synchronized void methodA() {
        //method A
    }

    public synchronized void methodB() {
        // method B
    }
}
```

## II. Explanation
Java Thread acquires an object level lock when it enters into an instance synchronized java method and acquires a class level lock when it enters into static synchronized java method.

In this case, the methods(instance) are of same class. So when ever a thread enters into java synchronized method or block it acquires a lock(the object on which the method is called). So other method cannot be called at the same time on the same object until the first method is completed and lock(on object) is released.

Putting synchronized on a method means the thread has to acquire the lock on the object instance before entering that method, so if you have two different methods marked synchronized the threads entering them will be contending for the same lock, and once one thread gets the lock all other threads are shut out of all methods that synchronize on that same lock. So in order for the two methods to run concurrently they would have to use different locks, like this:


```java
class A {
    private final Object lockA = new Object();
    private final Object lockB = new Object();

    public void methodA() {
        synchronized(lockA) {
            //method A
        }
    }

    public void methodB() {
        synchronized(lockB) {
            //method B
        }
    }
}
```


For more reference, see [Intrinsic Locks and Synchronization](https://docs.oracle.com/javase/tutorial/essential/concurrency/locksync.html)
