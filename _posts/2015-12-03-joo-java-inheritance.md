---
title: Java Inheritance
updated: 2015-12-03
---

 Inheritance can be defined as the process where one class **requires** the properties (**methods** and **fields**) of **another**. With the use of inheritance the information is made manageable in  a hierarchical order.

The class which inherits the properties of other is known as **subclass** (derived class, child class) as the class whose properties are inherited is known as **superclass** (base class, parent class).

## extends Keyword
**extends** is the keyword used to inherit the properties (methods and fields) of a class.

```java
class Super {
}

class Sub extends Super {
}
```

## The super keyword
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

## implements Keyword
Generally, the **implements** keyword is used with classes to inherit the properties of an **interface**. **interface** can **never** be **extended** by a class.

```java
public interface Animal {
}

public class Mammal implements Animal {
}

public class Dog extends Mammal {
}
```

## The instanceof Keyword

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

## Types of inheritance
The various type of inheritance as demonstrated below
![Types of inheritance](http://www.tutorialspoint.com/java/images/types_of_inheritance.jpg)

A very important fact to remember is that **Java does not support multiple inheritance**. This means, a class cannot extend more than one class.

However, **a class can implement one or more interfaces**.

##### [Java Site Map](../java-sitemap)
