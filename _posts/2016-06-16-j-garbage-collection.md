---
title: Java - Garbage Collection
updated: 2016-06-16
layout: single
categories:
  - java-garbage-collection
tags:
  - java-garbage-collection
---

## Introduction

In Java, allocation and de-allocation of memory space for objects are done by the garbage collection process in an automated way by the JVM.

Unlike C language the developers need not write code for garbage collection in Java. This is one among the many features that made Java popular and helps programmers write better Java applications.

### JVM architecture

Following diagram summarizes the key components in a JVM:

![jvm-architecture](http://javapapers.com/wp-content/uploads/2014/10/JVM-Architecture.jpg)

In the JVM architecture, two main components that are related to garbage collection are heap memory and garbage collector.

Heap memory is the runtime data area where the instances will be store and the garbage collector will operate on.

### Java Heap Memory

It is essential to understand the role of heap memory in JVM memory model. At runtime the Java instances are stored in the heap memory area. When an object is not referenced anymore it becomes eligible for eviction from heap memory. During garbage collection process, those objects are evicted from heap memory and the space is reclaimed. Heap memory has three major areas:

1. Young Generation

  * Eden Space (any instance enters the runtime memory area through eden)
  * S0 Survivor Space (older instances moved from eden to S0)
  * S1 Survivor Space (older instances moved from S0 to S1)
  
2. Old Generation (instances promoted from S1 to tenured)
3. Permanent Generation (contains meta information like class, method detail). **Note:** Permanent Generation (Permgen) space is removed from Java SE 8 features.

![java-heap-memory](http://javapapers.com/wp-content/uploads/2014/10/Java-Heap-Memory.jpg)

## References

* [javapapers-introduction-garbage-collection](#http://javapapers.com/java/java-garbage-collection-introduction/)