---
title: Java Inheritance
updated: 2015-12-03
categories:
  - java-object-oriented
tags:
  - java-object-oriented
---

Inheritance allows **code reuse** in Object oriented programming language.

Inheritance can be defined as the process where one class **requires** the properties (**methods** and **fields**) of **another**. With the use of inheritance the information is made manageable in a hierarchical order.

Inheritance in Java is supported using **extends** and **implements** keyword, **extends** keyword is used to inherit from another **Java Class** and allow to reuse functionality of Parent class. While **implements** keyword is used to implement **Interface** in Java.

The class which inherits the properties of other is known as **subclass** (derived class, child class) as the class whose properties are inherited is known as **superclass** (base class, parent class).

### Tables

* [extends Keyword](#extends-keyword-10548tables)
* [The super keyword](#the-super-keyword-10548tables)
* [implements Keyword](#implements-keyword-10548tables)
* [The instanceof Keyword](#the-instanceof-keyword-10548tables)
* [Types of inheritance](#types-of-inheritance-10548tables)
* [Importance points about Inheritance in Java](#importance-points-about-inheritance-in-java-10548tables)
* [When to use Inheritance in Java](#when-to-use-inheritance-in-java-10548tables)
* [References](#references-10548tables)

## extends Keyword [&#10548;](#tables)
**extends** is the keyword used to inherit the properties (methods and fields) of a class. When one class **extends** another class, it **inherit all non private members** including fields and method

```java
class Super {
}

class Sub extends Super {
}
```

## The super keyword [&#10548;](#tables)
The **super** keyword is used in:

* It is used to **differentiate the members** of superclass from the members of subclass, if they have same names.

  ```java
  super.variable
  super.method();
  ```

* It is used to **invoke the superclass** constructor from subclass. If a class is inheriting the properties of another class, the subclass automatically acquires the default constructor of the superclass. But if you want to **call a parametrized constructor** of the superclass, you need to use the **super keyword**

  ```java
  super(values);
  ```

## implements Keyword [&#10548;](#tables)
Generally, the **implements** keyword is used with classes to inherit the properties of an **interface**. **interface** can **never** be **extended** by a class.

```java
public interface Animal {
}

public class Mammal implements Animal {
}

public class Dog extends Mammal {
}
```

## The instanceof Keyword [&#10548;](#tables)

```java
interface Animal {}

class Mammal implements Animal {}

public class Dog extends Mammal {
    public static void main(String[] args) {
          Mammal m = new Mammal();
          Dog d = new Dog();

          System.out.println(m instanceof Animal);
          System.out.println(d instanceof Mammal);
          System.out.println(d instanceof Animal);
    }
}
// output is:
// true
// true
// true
```

## Types of inheritance [&#10548;](#tables)
The various type of inheritance as demonstrated below
![Types of inheritance](http://www.tutorialspoint.com/java/images/types_of_inheritance.jpg)

A very important fact to remember is that **Java does not support multiple inheritance**. This means, a class cannot extend more than one class.

However, **a class can implement one or more interfaces**.

## Importance points about Inheritance in Java [&#10548;](#tables)

1. Inheritance in Java is supported using **extends** and **implements** keyword, **extends** keyword is used to inherit from another **Java Class** and allow to reuse functionality of Parent class. While **implements** keyword is used to implement **Interface** in Java. Implementing an interface in Java doesn't actually meant for code reuse but provides Type hierarchy support. You can also use extends keyword when one interface extends another interface in Java.
2. If you **do not** want to allow Inheritance for your class then you can make it **final**. **final classes can not be extended** in Java and any attempt to inherit final class will result in compile time error.
3. **Constructor in Java are not inherited by Sub Class**. In face Constructors are chained, first statement in constructor is always a call to another constructor, either implicitly or explicitly. If you don't call any other constructor compiler will insert **super()**, which calls no argument constructor of super class in Java. this keyword represent current instance of class and super keyword represent instance of super class in Java.
4. Inheritance in Java represents **IS-A relationship**. If you see IS-A relationship between your domain Objects and Classes then consider using Inheritance e.g. if you have a class called ProgrammingLanguage than Java IS-A ProgrammingLanguage and should inherit from ProgrammingLanguage class.
5. **Private members** of **Super class** is **not visible** to **Sub class** even after using Inheritance in Java. Private members include any private field or method in Java.
6. Java has a special access modifier known as **protected** which is meant to support Inheritance in Java. Any protected member including protected method and field are only accessible in Child class or Sub class outside the package on which they are declared.
7. One of the **risk** of Inheritance in Java is that derived class can alter behavior of base class by overriding methods, which can compromise variants of base class e.g. if a malicious class overrides String's equals method in Java to change the comparison logic, you may get different behavior when String reference variable points to that class. to prevent such malicious overriding, you can make your class final to disallow inheritance. But beware making a class final severely implements its client's ability to reuse code. It make more sense from security perspective and that's one of the reason Why String is final in Java.
8. Use **@Override** annotation while overriding super class's method in subclass. This will ensure a compile time check on whether overriding method actually overrides super class method or not. Its common mistake to overload a method instead of overriding it mostly when super class method accept Object type, common examples are equals method, compareTo method and compare() method in Java.

## When to use Inheritance in Java [&#10548;](#tables)

* General policy to decide whether to use **Inheritance** or not is to check **IS-A** relationship. E.g. HashSet IS-A Set.
* Conversely if you find **HAS-A** relationship between two classes than use **Composition** e.g. *Car* HAS-A *Seat*.

## References [&#10548;](#tables)

* [javarevisited-inheritance](http://javarevisited.blogspot.com/2012/10/what-is-inheritance-in-java-and-oops-programming.html)