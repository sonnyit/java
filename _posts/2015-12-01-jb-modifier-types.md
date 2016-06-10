---
title: Java Basic - Modifier Types
updated: 2015-12-01
categories:
  - java
---

**Modifiers** are **keywords** that you **add to those definitions** to **change their meanings**. In Java language, we have:

* Java Access Modifiers
* Non Access Modifiers

To use a modifier, we include its **keyword** in the definition of a class, method, or variable.

## Java Access Control Modifiers
Java provides a number of **access modifiers** to **set access levels** for classes, variables, methods, and constructors. The four access levels are:

* **Default (no modifier):** visible to the package.
* **Private:** visible to the class only.
* **Public:** visible to the world.
* **Protected:** visible to the package and all subclasses.

| Access Modifiers | Same Class | Same Package | Sub Class | Other Package |
| ---------------- | ---------- | ------------ | --------- | ------------- |
| public  | Y | Y | Y | Y |
| protected | Y | Y | Y | N |
| no access modifier | Y | Y | N | N |
| private | Y | N | N | N |

## Non Access Modifiers
Java provides a number of non-access modifiers to achieve many other functionality.

* The **static** modifier for creating class methods and variables.
* The **final** modifier for finalizing the implementations of classes, methods and variables.
* The **abstract** modifier for creating abstract classes and methods.
* The **synchronized** and **volatile** modifiers, which are use for threads.

##### [Java Site Map](../java-sitemap)
