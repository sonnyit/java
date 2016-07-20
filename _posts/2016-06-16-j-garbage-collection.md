---
title: Java - Garbage Collection
updated: 2016-06-16
layout: single
categories:
  - java-garbage-collection
tags:
  - java-garbage-collection
---

### Tables

* [Introduction](#introduction-10548tables)
  * [Can the Garbage Collection be forced explicitly?](#can-the-garbage-collection-be-forced-explicitly-10548tables)
  * [Advantages of Garbage Collection](#advantages-of-garbage-collection-10548tables)
  * [JVM architecture](#jvm-architecture-10548tables)
  * [Java Heap Memory](#java-heap-memory-10548tables)
* [How Java Garbage Collection Works?](#how-java-garbage-collection-works-10548tables)
  * [Java Garbage Collection GC Initiation](#java-garbage-collection-gc-initiation-10548tables)
  * [Java Garbage Collection Process](#java-garbage-collection-process-10548tables)
  * [Finalization of Instances in Garbage Collection](#finalization-of-instances-in-garbage-collection-10548tables)
* [When an object becomes eligible for garbage collection?](#when-an-object-becomes-eligible-for-garbage-collection-10548tables)
* [References](#references-10548tables)

Garbage collection is responsible for removing objects from memory when they can never be used again. An object becomes eligible for garbage collection when there are no more references to it or its references have all gone out of scope. The **finalize()** method will run once for each object if/when it is  rst garbage collected.

## Introduction [&#10548;](#tables)

In Java, allocation and de-allocation of memory space for objects are done by the garbage collection process in an automated way by the JVM.

Unlike C language the developers need not write code for garbage collection in Java. This is one among the many features that made Java popular and helps programmers write better Java applications.

Java garbage collection is an automatic process to manage the runtime memory used by programs. By doing it automatic JVM relieves the programmer of the overhead of assigning and freeing up memory resources in a program.

### Can the Garbage Collection be forced explicitly?

No, the Garbage Collection can not be forced explicitly. We **may request** JVM for garbage collection by calling **System.gc()** or **Runtime.gc()** method. But this **does not guarantee** that JVM will perform the garbage collection.

### Advantages of Garbage Collection

1. Programmer doesn't need to worry about dereferencing an object.
2. It is done automatically by JVM.
3. Increases memory efficiency and decreases the chances for memory leak.

### JVM architecture [&#10548;](#tables)

Following diagram summarizes the key components in a JVM:

![jvm-architecture](http://javapapers.com/wp-content/uploads/2014/10/JVM-Architecture.jpg)

In the JVM architecture, two main components that are related to garbage collection are heap memory and garbage collector.

Heap memory is the runtime data area where the instances will be store and the garbage collector will operate on.

### Java Heap Memory [&#10548;](#tables)

It is essential to understand the role of heap memory in JVM memory model. At runtime the Java instances are stored in the heap memory area. When an object is not referenced anymore it becomes eligible for eviction from heap memory. During garbage collection process, those objects are evicted from heap memory and the space is reclaimed. Heap memory has three major areas:

1. Young Generation
  * Eden Space (any instance enters the runtime memory area through eden)
  * S0 Survivor Space (older instances moved from eden to S0)
  * S1 Survivor Space (older instances moved from S0 to S1)
2. Old Generation (instances promoted from S1 to tenured)
3. Permanent Generation (contains meta information like class, method detail). **Note:** Permanent Generation (Permgen) space is removed from Java SE 8 features.

![java-heap-memory](http://javapapers.com/wp-content/uploads/2014/10/Java-Heap-Memory.jpg)

## How Java Garbage Collection Works? [&#10548;](#tables)

### Java Garbage Collection GC Initiation [&#10548;](#tables)

Being an automatic process, programmers need not initiate the garbage collection process explicitly in the code. **System.gc()** and **Runtime.gc()** are hooks to request the JVM to initiate the garbage collection process.

Though this request mechanism provides an opportunity for the programmer to initiate the process but the onus is on the JVM. It can choose to reject the request and so it is not guaranteed that these calls will do the garbage collection. This decision is taken by the JVM based on the eden space availability in heap memory. The JVM specification leaves this choice to the implementation and so these details are implementation specific.

Undoubtedly we know that the garbage collection process cannot be forced.

### Java Garbage Collection Process [&#10548;](#tables)

Garbage collection is the process of reclaiming the unused memory space and making it available for the future instances.

![garbage-collection-process](http://javapapers.com/wp-content/uploads/2014/10/Java-Garbage-Collection-Process3_thumb.jpg)

#### Eden Space

When an instance is created, it is first stored in the eden space in young generation of heap memory area.

#### Survivor Space (S0 and S1)

As part of the minor garbage collection cycle, objects that are live (which is still referenced) are moved to survivor space S0 from eden space. Similarly the garbage collector scans S0 and moves the live instances to S1.

Instances that are not live (dereferenced) are marked for garbage collection. Depending on the garbage collector (there are four types of garbage collectors available) chosen either the marked instances will be removed from memory on the go or the eviction process will be done in a separate process.

#### Old Generation

Old or tenured generation is the second logical part of the heap memory. When the garbage collector does the minor GC cycle, instances that are still live in the S1 survivor space will be promoted to the old generation. Objects that are dereferenced in the S1 space is marked for eviction.

#### Major GC

Old generation is the last phase in the instance life cycle with respect to the Java garbage collection process. Major GC is the garbage collection process that scans the old generation part of the heap memory. If instances are dereferenced, then they are marked for eviction and if not they just continue to stay in the old generation.

#### Memory Fragmentation

Once the instances are deleted from the heap memory the location becomes empty and becomes available for future allocation of live instances. These empty spaces will be fragmented across the memory area. For quicker allocation of the instance it should be defragmented. Based on the choice of the garbage collector, the reclaimed memory area will either be compacted on the go or will be done in a separate pass of the GC.

### Finalization of Instances in Garbage Collection [&#10548;](#tables)

Just before evicting an instance and reclaiming the memory space, the Java garbage collector invokes the **finalize()** method of the respective instance so that the instance will get a chance to free up any resources held by it.

Though there is a guarantee that the finalize() will be invoked before reclaiming the memory space, there is **no order or time specified**. The order between multiple instances cannot be predetermined, they can even happen in parallel. Programs should not pre-mediate an order between instances and reclaim resources using the finalize() method.

* Any uncaught exception thrown during finalize process is ignored silently and the finalization of that instance is cancelled.
* JVM specification does not discuss about garbage collection with respect to weak references and claims explicitly about it. Details are left to the implementer.
* Garbage collection is done by a daemon thread.

#### finalize() method

Sometime an object will need to perform some specific task before it is destroyed such as closing an open connection or releasing any resources held. To handle such situation **finalize()** method is used. **finalize()** method is called by garbage collection thread before collecting object. Its the last chance for any object to perform cleanup utility.

Signature of **finalize()** method

```java
protected void finalize() {
 //finalize-code
}
```

#### Some Important Points to Remember

1. **finalize()** method is defined in **java.lang.Object** class, therefore it is available to all the classes.
2. **finalize()** method is declare as **proctected** inside Object class.
3. **finalize()** method gets called only once by GC threads.

## When an object becomes eligible for garbage collection? [&#10548;](#tables)

* Any instances that cannot be reached by a live thread.
* Circularly referenced instances that cannot be reached by any other instances.

There are different types of references in Java. Instances eligibility for garbage collection depends on the type of reference it has.

| Reference	Garbage | Collection |
| ----------------- | ---------- |
| Strong Reference | Not eligible for garbage collection |
| Soft Reference	| Garbage collection possible but will be done as a last option |
| Weak Reference |	Eligible for Garbage Collection |
| Phantom Reference |	Eligible for Garbage Collection |

## References [&#10548;](#tables)

* [javapapers-introduction-garbage-collection](#http://javapapers.com/java/java-garbage-collection-introduction/)
* [javapapers-garbage-collection-works](http://javapapers.com/java/how-java-garbage-collection-works/)