---
title: Java - Reference Types
updated: 2016-06-16
layout: single
categories:
  - java-garbage-collection
tags:
  - java-garbage-collection
---

There are four types of references in Java.

### Tables

* [Strong Reference](#strong-reference-10548tables)
* [Weak Reference](#weak-reference-10548tables)
* [Soft Reference](#soft-reference-10548tables)
* [Phantom Reference](#phantom-reference-10548tables)
* [Topic Related](#topic-related-10548tables)

## Strong Reference [&#10548;](#tables)

These type of references we use daily while writing the code. Any object in the memory which has active **strong reference is not eligible for garbage collection**.

```java
class A {
    //Class A
}
 
public class MainClass {
    public static void main(String[] args) {
        A a = new A();    //Strong Reference - at this point, this object can't be garbage collected
        a = null;    //Now, object to which 'a' is pointing earlier is eligible for garbage collection.
    }
}
```

If you make reference **'a'** to point to null, then, object to which ‘a’ is pointing earlier will become eligible for garbage collection. Because, it will have no active references pointing to it. This object is most likely to be garbage collected when garbage collector decides to run.

![strong-reference](http://javaconceptoftheday.com/wp-content/uploads/2015/02/StrongReference.png)

## Soft Reference [&#10548;](#tables)

The objects which are **softly referenced will not be garbage collected** (even though they are available for garbage collection) **until JVM badly needs memory**.

These objects will be cleared from the memory only if JVM runs out of memory.

You can create a soft reference to an existing object by using **java.lang.ref.SoftReference** class. 

```java
class A {
    //A Class
}
 
public class MainClass {
    public static void main(String[] args) {
        A a = new A();      //Strong Reference
        //Creating Soft Reference to A-type object to which 'a' is also pointing
        SoftReference<A> softA = new SoftReference<A>(a);
        a = null;    //Now, A-type object to which 'a' is pointing earlier is eligible for garbage collection. But, it will be garbage collected only when JVM needs memory.
        a = softA.get();    //You can retrieve back the object which has been softly referenced
    }
}
```

In the above example, you create two strong references – 'a' and 'softA'. 'a' is pointing to A-type object and 'softA' is pointing to SoftReference type object. This SoftReference type object is internally referring to A-type object to which 'a' is also pointing.

When 'a' is made to point to null, object to which 'a' is pointing earlier becomes eligible for garbage collection. But, it will be garbage collected only when JVM needs memory. Because, it is softly referenced by 'softA' object.

![soft-reference](http://javaconceptoftheday.com/wp-content/uploads/2015/02/SoftReference.png)

## Weak Reference [&#10548;](#tables)

**JVM ignores the weak references**. That means objects which has only **week references are eligible for garbage collection**. They are likely to be garbage collected when JVM runs garbage collector thread.

```java
class A {
    //A Class
}
 
public class MainClass {
    public static void main(String[] args) {
        A a = new A();      //Strong Reference
        //Creating Weak Reference to A-type object to which 'a' is also pointing.
        WeakReference<A> weakA = new WeakReference<A>(a);
        a = null;    //Now, A-type object to which 'a' is pointing earlier is available for garbage collection.
        a = weakA.get();    //You can retrieve back the object which has been weakly referenced.
    }
}
```

![weak-reference](http://javaconceptoftheday.com/wp-content/uploads/2015/02/WeakReference.png)

## Phantom Reference [&#10548;](#tables)

The objects which are being referenced by **phantom references** are **eligible for garbage collection**. But, before removing them from the memory, JVM puts them in a queue called **'reference queue'** . They are put in a reference queue after calling finalize() method on them. You can't retrieve back the objects which are being phantom referenced. That means calling get() method on phantom reference always returns null.

```java
class A {
    //A Class
}
 
public class MainClass {
    public static void main(String[] args) {
        A a = new A();      //Strong Reference
        //Creating ReferenceQueue
        ReferenceQueue<A> refQueue = new ReferenceQueue<A>();
        //Creating Phantom Reference to A-type object to which 'a' is also pointing
        PhantomReference<A> phantomA = new PhantomReference<A>(a, refQueue);
        a = null;    //Now, A-type object to which 'a' is pointing earlier is available for garbage collection. But, this object is kept in 'refQueue' before removing it from the memory.
        a = phantomA.get();    //it always returns null
    }
}
```

## Topic Related [&#10548;](#tables)

* [javaconceptoftheday-types-of-references](http://javaconceptoftheday.com/types-of-references-in-java-strong-soft-weak-and-phantom/)
* [javapapers-reference](http://javapapers.com/core-java/java-weak-reference/)