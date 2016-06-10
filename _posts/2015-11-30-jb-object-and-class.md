---
title: Java Basic - Objects & Classes
updated: 2015-11-30
---

Java is an Object-Oriented Language. As a language that has Object Oriented feature, java supports the following fundamental concepts:

* Polymorphism
* Inheritance
* Encapsulation
* Abstraction
* Classes
* Objects
* Instance
* Method
* Message Parsing

In this part, we will look into the concepts of Classes and Objects.

## Objects in Java

* Objects have states and behaviors.
* State is stored in fields and behavior is shown via methods.
* So, methods operate on the internal state of an object and the object-to-object communication is done via methods.

## Classes in Java

A class is a blue print from which individual objects are created.
A class can contain any of the following variable types.

* **Local variables:**
     * Variables are defined inside methods, constructors or blocks are called local variables.
     * Will be declared and initialized within the method and the variable will be destroyed when the method has completed.
* **Instance variables:**
    * Instance variables are variables within a class but outside any method.
    * These variables are initialized when a class is instantiated.
    * Instance variables can be accessed from inside any method, constructor or blocks of that particular class.
* **Class variables:**
    * Class variables declared within a class, **outside any method**, with the **static keyword**.

## Constructor
* Every class has a constructor.
* If we do not explicitly write a constructor for a class, the Java compiler builds a default constructor for that class.
* Each time a new object is created, at least one constructor will be invoked.
* The constructors must have the same name as the class.
* A class can have more than one constructor.

## Creating an Object
Three steps when creating an object from a class:

* **Declaration:** a variable declaration with: a variable name and an object type.
* **Instantiation:** The **new** keyword is used to create the object.
* **Initialization:** The **new** keyword **is followed by a call to a constructor**. This call initializes the new object.

## Source file declaration rules:
These rules are essential when declaring classes, *import* statements and *package* statements in a source file:

* There can be only one public class per source file.
* A source file can have multiple non public classes.
* A public class name should be the name of source file as well which should be appended by **.java** at the end. For example: the class name is *public class Employee{}* then the source file should be as Employee.java
* If the class is defined inside a package, then the package statement should be the first statement in the source file.
* If import statement are present then they must be written between the package statement and the class declaration. If there are no package statements then the import statement should be the first line in the source file.
* Import and package statements will imply to all the classes present in the source file. It is not possible to declare different import and/or package statements to different classes in the source file.

## Java package
In simple, it is a way of categorizing the classes and interfaces. When developing applications in Java, hundreds of classes and interfaces will be written, therefore categorizing these classes is a must as well as makes life much easier.

## Import statements
In Java if a fully qualified name, which includes the package and the class name, is given then the compiler can easily locate the source code or classes. Import statement is a way of giving the proper location for the compiler to find that particular class.

For example, the following line would ask compiler to load all the classes available in directory java_installation/java/io:

```java
import java.io.*;
```

##### [Java Site Map](../java-sitemap)
