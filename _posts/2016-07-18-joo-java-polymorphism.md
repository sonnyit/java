---
title: Java Polymorphism
updated: 2016-07-19
categories:
  - java-object-oriented
tags:
  - java-object-oriented
---

Polymorphism is the ability of an object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.

Any Java object that can pass more than one IS-A test is considered to be polymorphic. In Java, all Java objects are polymorphic since any object will pass the IS-A test for their own type and for the class Object.

![polymorphism](http://www.javatpoint.com/images/polymorphism.gif)

### Tables

* [Example](#example-10548tables)
* [How Polymorphism supported in Java](#how-polymorphism-supported-in-java-10548tables)
* [References](#references-10548tables)

## Example

```java
public interface Vegetarian {}
public class Animal {}
public class Deer extends Animal implements Vegetarian {}
```
Now, the Deer class is considered to be polymorphic since this has multiple inheritance. Following are true for the above example:

* A Deer IS-A Animal
* A Deer IS-A Vegetarian
* A Deer IS-A Deer
* A Deer IS-A Object

When we apply the reference variable facts to a Deer object reference, the following declarations are legal:

```java
Deer d = new Deer();
Animal a = d;
Vegetarian v = d;
Object o = d;
```

All the reference variables d,a,v,o refer to the same Deer object in the heap.

Polymorphism is only for instance method not for instance variable.

## How Polymorphism supported in Java

Java has excellent support of polymorphism in terms of Inheritance, method overloading and method overriding.

In case of overloading method signature changes while in case of overriding method signature remains same and binding and invocation of method is decided on runtime based on actual object. This facility allows Java programmer to write very flexibly and maintainable code using interfaces without worrying about concrete implementation.

## References
* [tutorialspoint-polymorphism](http://www.tutorialspoint.com/java/java_polymorphism.htm)
* [javarevisited-polymorphism](http://javarevisited.blogspot.com/2011/08/what-is-polymorphism-in-java-example.html)