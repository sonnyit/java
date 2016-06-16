---
title: Java - Types of Garbage Collectors
updated: 2016-06-16
layout: single
categories:
  - java-garbage-collection
tags:
  - java-garbage-collection
---

### Tables

* [Introduction](#introduction-10548tables)
* [Serial Garbage Collector](#serial-garbage-collector-10548tables)
* [Parallel Garbage Collector](#parallel-garbage-collector-10548tables)
* [CMS Garbage Collector](#cms-garbage-collector-10548tables)
* [G1 Garbage Collector](#g1-garbage-collector-10548tables)
  * [Java 8 Improvement](#java-8-improvement-10548tables)
* [Garbage Collection JVM Options](#garbage-collection-jvm-options-10548tables)
  * [Type of Garbage Collector to run](#type-of-garbage-collector-to-run-10548tables)
  * [GC Optimization Options](#gc-optimization-options-10548tables)
  * [Example Usage of JVM GC Options](#example-usage-of-jvm-gc-options-10548tables)
* [References](#references-10548tables)

## Introduction [&#10548;](#tables)

Java has four types of garbage collectors. Each of these four types has its own advantages and disadvantages.

Most importantly, the programmers can choose the type of garbage collector to be used by the JVM.

We can choose them by passing the choice as JVM argument. Each of these types differ largely and can provide completely different application performance. It is critical to understand each of these types of garbage collectors and use it rightly based on the application.

![types-of-garbage-collectors](http://javapapers.com/wp-content/uploads/2014/10/Types-of-Java-Garbage-Collectors3_th_thumb.jpg)

## Serial Garbage Collector [&#10548;](#tables)

Serial garbage collector works by holding all the application threads. It is designed for the single-threaded environments.

It uses just a single thread for garbage collection. The way it works by freezing all the application threads while doing garbage collection may not be suitable for a server environment. It is best suited for simple command-line programs.

Turn on the **-XX:+UseSerialGC** JVM argument to use the serial garbage collector.

## Parallel Garbage Collector [&#10548;](#tables)

Parallel garbage collector is also called as throughput collector. **It is the default garbage collector of the JVM**.

Unlike serial garbage collector, this uses multiple threads for garbage collection. Similar to serial garbage collector this also freezes all the application threads while performing garbage collection.

## CMS Garbage Collector [&#10548;](#tables)

Concurrent Mark Sweep (CMS) garbage collector uses multiple threads to scan the heap memory to mark instances for eviction and then sweep the marked instances. CMS garbage collector holds all the application threads in the following two scenarios only:

* while marking the referenced objects in the tenured generation space.
* if there is a change in heap memory in parallel while doing the garbage collection.

In comparison with parallel garbage collector, CMS collector uses more CPU to ensure better application throughput. If we can allocate more CPU for better performance then CMS garbage collector is the preferred choice over the parallel collector.

Turn on the **XX:+USeParNewGC** JVM argument to use the CMS garbage collector.

## G1 Garbage Collector [&#10548;](#tables)

G1 garbage collector is used for large heap memory areas. It separates the heap memory into regions and does collection within them in parallel. G1 also does compacts the free heap space on the go just after reclaiming the memory. But CMS garbage collector compacts the memory on stop the world (STW) situations. G1 collector prioritizes the region based on most garbage first.

Turn on the **–XX:+UseG1GC** JVM argument to use the G1 garbage collector.

#### Java 8 Improvement [&#10548;](#tables)

Turn on the **-XX:+UseStringDeduplication** JVM argument while using **G1** garbage collector. This optimizes the heap memory by removing duplicate String values to a single char[] array. This option is introduced in Java 8u 20.

## Garbage Collection JVM Options [&#10548;](#tables)

Following are the key JVM options that are related to Java garbage collection.

### Type of Garbage Collector to run [&#10548;](#tables)

| Option	| Description |
| ------- | ----------- |
| -XX:+UseSerialGC |	Serial Garbage Collector |
| -XX:+UseParallelGC |	Parallel Garbage Collector |
| -XX:+UseConcMarkSweepGC |	CMS Garbage Collector |
| -XX:ParallelCMSThreads=	| CMS Collector – number of threads to use |
| -XX:+UseG1GC	| G1 Gargbage Collector |

### GC Optimization Options [&#10548;](#tables)

| Option |	Description |
| ------ | ------------ |
| -Xms |	Initial heap memory size |
| -Xmx |	Maximum heap memory size |
| -Xmn |	Size of Young Generation |
| -XX:PermSize |	Initial Permanent Generation size |
| -XX:MaxPermSize |	Maximum Permanent Generation size |

### Example Usage of JVM GC Options [&#10548;](#tables)

```bash
$java -Xmx12m -Xms3m -Xmn1m -XX:PermSize=20m -XX:MaxPermSize=20m -XX:+UseSerialGC -jar java-application.jar
```

## References [&#10548;](#tables)

* [javapapers-types-of-java-garbage-colletors](http://javapapers.com/java/types-of-java-garbage-collectors/)