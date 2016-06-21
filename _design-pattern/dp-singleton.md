---
title: Design Pattern - Singleton
updated: 2016-06-20
layout: single
categories:
  - java-design-pattern
tags:
  - java-design-pattern
---

Singleton pattern is one of the most commonly used patterns in Java. It is used to control the number of objects created by preventing external instantiation and modification. This concept can be generalized to systems that operate more efficiently when only one object exists, or that restrict the instantiation to a certain number of objects, such as: single DB connection, single configuration manager, error manager, etc.

### Tables

* [Definition](#definition-10548tables)
* [Implementation](#implementation-10548tables)
  * [Method 1: Classic Implementation](#method-1-classic-implementation-10548tables)
  * [Method 2: make getInstance() synchronized](#method-2-make-getinstance-synchronized-10548tables)
  * [Method 3: Eager Instantiation](#method-3-eager-instantiation-10548tables)
  * [Method 4 (Best): Use "Double Checked Locking"](#method-4-best-use-double-checked-locking-10548tables)
  * [Another Implementation of Singleton Pattern](#another-implementation-of-singleton-pattern-10548tables)
* [References](#references-10548tables)

## Definition [&#10548;](#tables)

The **Singleton pattern** is a design pattern that *restricts the instantiation of a class to one object*.

Let’s see various design options for implementing such a class. If you have a good handle on static class variables and access modifiers this should not be a difficult task.

## Implementation [&#10548;](#tables)

### Method 1: Classic Implementation [&#10548;](#tables)

```java
// Classical Java implementation of singleton 
// design pattern
class Singleton
{
    private static Singleton obj;
 
    // private constructor to force use of
    // getInstance() to create Singleton object
    private Singleton() {}
 
    public static Singleton getInstance()
    {
        if (obj==null)
            obj = new Singleton();
        return obj;
    }
}
```

* Here we have declared getInstance() static so that we can call it without instantiating the class.
* The first time getInstance() is called it creates a new singleton object and after that it just returns the same object.
* **Note that** Singleton obj is not created until we need it and call getInstance() method. This is called lazy instantiation.

The main problem with above method is that it is not thread safe. Consider the following execution sequence.

![singleton](http://d1gjlxt8vb0knt.cloudfront.net//wp-content/uploads/singleton.png)

This execution sequence creates two objects for singleton. Therefore this **classic implementation** is not **thread safe**.

### Method 2: make getInstance() synchronized [&#10548;](#tables)

```java
// Thread Synchronized Java implementation of 
// singleton design pattern
class Singleton
{
    private static Singleton obj;
 
    private Singleton() {}
 
    // Only one thread can execute this at a time
    public static synchronized Singleton getInstance()
    {
        if (obj==null)
            obj = new Singleton();
        return obj;
    }
}
```

* Here using **synchronized** makes sure that only **one thread** at a time can **execute getInstance()**.
* The **main disadvantage** of this is method is that **using synchronized every time** while creating the singleton object is **expensive** and may decrease the performance of your program. However if performance of getInstance() is not critical for your application this method provides a clean and simple solution.

### Method 3: Eager Instantiation [&#10548;](#tables)

```java
// Static initializer based Java implementation of
// singleton design pattern
class Singleton
{
    private static Singleton obj = new Singleton();
 
    private Singleton() {}
 
    public static Singleton getInstance()
    {
        return obj;
    }
}
```

* Here we have created instance of singleton in **static initializer**.
* JVM executes **static initializer** when the **class is loaded** and hence this is **guaranteed to be thread safe**. Use this method only when your singleton class is light and is used throughout the execution of your program.

### Method 4 (Best): Use "Double Checked Locking" [&#10548;](#tables)

If you notice carefully once an object is created synchronization is no longer useful because now obj will not be null and any sequence of operations will lead to consistent results.

So we will only acquire lock on the getInstance() once, when the obj is null. This way we only synchronize the first way through, just what we want.

```java
// Double Checked Locking based Java implementation of
// singleton design pattern
class Singleton
{
    private volatile static Singleton obj;
 
    private Singleton() {}
 
    public static Singleton getInstance()
    {
        if (obj == null)
        {
            // To make thread safe
            synchronized (Singleton.class)
            {
                // check again as multiple threads
                // can reach above step
                if (obj==null)
                    obj = new Singleton();
            }
        }
        return obj;
    }
}
```

* We have declared the obj [volatile](http://www.geeksforgeeks.org/volatile-keyword-in-java/) which ensures that multiple threads offer the obj variable correctly when it is being initialized to Singleton instance.
* This method drastically reduces the overhead of calling the synchronized method every time.

### Another Implementation of Singleton Pattern [&#10548;](#tables)

As private constructor doesn't protect from instantiation via reflection, Joshua Bloch (Effective Java) proposes a better implementation of Singleton. If you are not familiar with Enum, here is a good example from Oracle.

```java
public enum AmericaPresident{
	INSTANCE;
 
	public static void doSomething(){
		//do something
	}
}
```

## References [&#10548;](#tables)
* [geeksforgeeks-singleton](http://www.geeksforgeeks.org/singleton-design-pattern/)
* [programcreek-singleton](http://www.programcreek.com/2011/07/java-design-pattern-singleton/)