---
title: Java Basic - Basic Syntax
updated: 2015-12-01
categories:
  - java
---


A Java program it can be defined as **a collection of objects** that **communicate** via **invoking** each **other's methods**.

* **Object -** Objects have **states** and **behaviors**.
* **Class -** A class can be defined as a template/blue print that describles the behaviors/states that object of its type support.
* **Methods -** A methods is basically a behavior. A class can contain many methods.
* **Instance Variables -** Each object has its unique set of instance variables. An object's state is create by the values assigned to these instance variables.

## Example First Java Program

```java
public class MyFirstJavaProgram {
    /* This is my first java program. 
    * This will print 'Hello World' as the output
    */
    public static void main(String []args) {
    System.out.println("Hello World"); // prints Hello World
    }
} 
```

Put this code in a file's name "MyFirstJavaProgram.java" (must exactly typo). Compile and run with:

```bash
javac MyFirstJavaProgram.java
java MyFirstJavaProgram
Hello World
```

## Basic Syntax
With Java programs, it is **very important** to keep in mind the following points:

* **Case Sensitivity -** Java is case sensitive, so **Hello** and **hello** have different meaning in Java.
* **Class Names -** For all class names, the **first letter** should be in **Upper Case**. Ex: *MyFirstJavaClass*.
* **Method Names -** All method names should start with a **Lower Case** letter. Ex: *public void myMethodName()*.
* **Program File Name -** Name of the program file should **exactly match** the (only) **public class name** in this file. Ex: assume 'MyFirstJavaProgram' is the class name. Then the file should be saved as 'MyFirstJavaProgram.java'.
* **public static void main(String args[]) -** Java program processing starts from the main() methods which is a mandatory part of every Java program.

## Java Identifiers
In Java, we have several points that will need to remember about identifiers:

* All identifiers should begin with a letter **(A-Z or a-z)**, currency character **$** or underscore **_**.
* After the first character, identifiers can have any combination of character.
* Identifier **cannot** have the same name with any **keyword**.
* Most importantly identifiers are case sensitive.
* Example of **legal** identifiers:  age, $salary, _value, __1_value.
* Example of **illegal** identifiers: 123abc, -salary.

## Java Modifiers
Like other languages, it is possible to modify classes, methods, etc., by using modifiers. There are two categories of modifiers:

* **Access Modifiers:** default, public, protected, private.
* **Non-access Modifiers:** final, abstract, strictfp.

## Java Variables
Types of variables in Java are:

* Local Variables
* Class Variables (Static Variables)
* Instance Variables (Non-static variables)

## Java Arrays
**Arrays** are **objects** that **store** multiple variables of the **same type**. However, an array itself is an object **on the heap**.

## Java Enums
Enums were introduced in Java 5.0. Enums restrict a variable to have **one of only a few predefined values**. The values in this enumerated list are called enums.

**Note:**
* Enums can be declared as **their own** or **inside a class**.
* Methods, variables, constructors can be defined inside enums as well.

## Inheritance
In Java, classes can be derived from classes.

This concept allows you to reuse the fields and methods of the existing class without having to rewrite this code in a new class. In this scenario:

* The existing class is called the superclass.
* The derived class is called the subclass.

## Interfaces
In Java language, an interface can by defined as a contract between objects on how to communicate with each other. Interfaces play a vital role when it comes to the concept of inheritance.

An interface defines the methods, a deriving class (subclass) should use. But the implementation of the methods is totally up to the subclass.

##### [Java Site Map](../java-sitemap)
