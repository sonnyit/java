---
title: Java Abstract
updated: 2015-12-02
categories:
  - java-object-oriented
tags:
  - java-object-oriented
---

Abstraction is the concept of exposing only the required essential characteristics and behavior with respect to a context.

### Tables

* [What is Abstraction?](#what-is-abstraction-10548tables)
* [When do you use Abstraction?](#when-do-you-use-abstraction-10548tables)
* [Java Abstract Class](#java-abstract-class-10548tables)
	* [When Should I use an Abstract class](#when-should-i-use-an-abstract-class-10548tables)
* [Abstraction Using Interface in Java](#abstraction-using-interface-in-java-10548tables)
* [More about Java Abstract](#more-about-java-abstract-10548tables)
	* [Java Abstract Method](#java-abstract-method-10548tables)
	* [Extending an Abstract Class](#extending-an-abstract-class-10548tables)
	* [Abstract class Implements an Interface](#abstract-class-implements-an-interface-10548tables)
	* [Can an Abstract Class have Constructor in Java?](#can-an-abstract-class-have-constructor-in-java-10548tables)
	* [Can an Abstract class be final in Java?](#can-an-abstract-class-be-final-in-java-10548tables)
* [Difference between Abstraction and Encapsulation in Java](#difference-between-abstraction-and-encapsulation-in-java-10548tables)
* [Abstraction: Things to Remember](#abstraction-things-to-remember-10548tables)
* [References](#references-10548tables)

## What is Abstraction? [&#10548;](#tables)

Abstraction in Java or Object oriented programming is a way to segregate *implementation* from *an interface* and one of the five fundamentals along with Encapsulation, Inheritance, Polymorphism, Class, and Object.

Abstraction in Java is achieved by using **interface** and **abstract class** in Java.

An interface or abstract class is something which is not concrete, something which is incomplete.

In order to use interface or abstract class, we need to extend and implement an abstract method with concrete behavior.

One example of Abstraction is creating interface to denote common behavior without specifying any details about how that behavior works e.g. You create an interface called Server which has the start() and stop() method. This is called abstraction of Server because every server should have a way to start and stop and details may differ.

## When do you use Abstraction? [&#10548;](#tables)

When you know something needs to be there but not sure how exactly it should look like.

Ex: when creating a class called *Vehicle*, I know there should be methods like *start()* and *stop()* but don't know how that start and stop method should work, because every vehicle can have different start and stop mechanism e..g some can be started by kicking or some can be by pressing buttons. So the implementation of those start() and stop() methods should be left to their concrete implementation e.g. Scooter, MotorBike , Car etc.

## Java Abstract Class [&#10548;](#tables)

* An abstract class is something which is incomplete and you **can not create an instance** of the **abstract class**. If you want to use it you need to make it complete or concrete by **extended** it.
* A **Java class** that is declared using the keyword **abstract** is called an **abstract class**.
* An abstract class can have abstract methods and concrete methods or both. Methods with implementation body are concrete methods. But if a class have at least one abstract method, then the class **must** be declared **abstract**.
	* An abstract method in Java doesn't have the body , it's just a declaration. In order to use an abstract method, you need to override that method in sub class.
* Java has a concept of abstract classes, abstract method but a variable can not be abstract in Java.
* An abstract class can have *static fields* and *methods* and they can be used the same way as used in a concrete class.
* To use an abstract class you have to inherit it from another class, provide implementations to the abstract methods in it.

```java
public abstract class Animal {
}
```

### When Should I use an Abstract class [&#10548;](#tables)
We should go for abstract class when we are working with **classes** that **contains similar code**. That is, there is a possibility to template behavior and attributes. So, what we gain from this template pattern is avoiding repetition of common code.

Common behavior can be elevated to a super class and provide implementation to it. Then add behavior that cannot be implemented and declare it as abstract. Classes that are similar to this abstract class will extend it and use the already implemented methods and add implementation for abstract methods.

## Abstraction Using Interface in Java [&#10548;](#tables)

* In Java Interface is an another way of providing abstraction.
* Interfaces are by default abstract and only contains *public, static, final constant or abstract methods*.

### It's very common interview question is that: "where should we use abstract class and where should we use Java Interfaces?"

You can go for java interface if you only know the name of methods your class should have e.g. for Server it should have start() and stop() method but we don't know how exactly these start and stop method will work. 

If you know some of the behavior while designing class and that would remain common across all subclasses add that into an abstract class.

An interface like Runnable interface is a good example of abstraction in Java which is used to abstract task executed by multiple threads. Callable is another good abstract of a task which can return value. 

## More about Java Abstract [&#10548;](#tables)

### Java Abstract Method [&#10548;](#tables)
A method that is declared using the keyword **abstract** is called an **abstract method**.

Abstract methods are declaration only and it will not have implementation. It will not have a method body.

A Java class containing an abstract method must be declared as abstract class.

Any class inheriting the current class must either override the abstract method or declare itself as abstract.

An abstract method can only set a **visibility modifier**, among *public* or *protected*.

An abstract method cannot add **static** or **final** modifier to the declaration.

```java
public abstract class Animal {
    String name;

    public abstract String getSound();

    public String getName() {
          return name;
    }
}
```

### Extending an Abstract Class [&#10548;](#tables)
When an abstract class is implemented in Java, generally all its abstract methods will be defined. If one or more abstract method is not defined in the implementing class, then it also should be declared as an abstract class too.

Following is an example class that implements the Animal abstract class. **@Override** is a **Java annotation** used to state that this method overrides the method in the super class.

```java
public class Lion extends Animal {
    @Override
    public String getSound() {
          return "roar";    
     }
}
```

### Abstract class Implements an Interface [&#10548;](#tables)
![Abstract class Implements an Interface](http://javapapers.com/wp-content/uploads/2015/07/Java-Abstract-Class-and-Methods.jpg)

It is **possible** for an *abstract* class to **implement** a Java *interface*. If the implementing class does not implement all of the abstract methods from the interface, then this must be defined an *abstract* class in Java.

Difference between an *interface* and *abstract* class is methods in an interface are implicitly abstract.

```java
public interface Species {
    public String getClassification();
}

public abstract class Animal implements Species {
    String name;
    public String getName() {
        return name;
    }
}
```

So, Animal class does not implement the abstract method (getClassification) from Species interface. Though Animal does not have any abstract method on its own, it must be declared as abstract since it did not implement the abstract method from Species interface. Any class that extends the Animal class should implement the getClassification abstract method.

### Can an Abstract Class have Constructor in Java? [&#10548;](#tables)
**Yes,** an abstract class can have constructor in Java. It can be a useful option to enforce class constraints like setting up a field.

```java
public abstract class Animal {
    String name;

    public Animal(String name) {
          this.name = name;
    }

    public String getName() {
          return name;
    }

    public abstract String getSound();
}
```

This abstract class defines a constructor with an argument that is used to setup the field name. Classes that extends this abstract class should define a constructor with implicit **super()** call to the super abstract class. Otherwise we will get an error as "implicit super constructor Animal() is undefined. Must explicitly invoke another constructor". This is to do some initialization before instantiation.

```java
public class Lion extends Animal {
    public Lion(String name) {
          super(name);
    }

    @Override
    public String getSound() {
          return "roar";
    }
}
```

### Can an Abstract class be final in Java? [&#10548;](#tables)
**No,** an abstract class cannot be declared as **final** in Java. Because it will completely negate the purpose of an abstract class.

An abstract class should be extended to create instances. If it is declared final, then it cannot be extended and so an abstract class cannot be declared as final.

## Difference between Abstraction and Encapsulation in Java [&#10548;](#tables)

1. First difference between Abstraction and Encapsulation is that, Abstraction is implemented in Java using interface and abstract class while Encapsulation is implemented using private, package-private and protected access modifier.
2. Encapsulation is also called data hiding.
3. Design principles "programming for interface than implementation" is based on abstraction and "encapsulate whatever changes" is based upon Encapsulation.

## Abstraction: Things to Remember [&#10548;](#tables)

1. Use abstraction if you know something needs to be in class but the implementation of that varies. Abstraction is actually resulting of thought process and it really need good experience of both domain and Object oriented analysis and design to come up with good abstraction for your project.
2. In Java, you can not create an instance of the abstract class using the new operator, its compiler error. Though abstract class can have a constructor.
3. **abstract** is a keyword in Java, which can be used with both class and method.  Abstract class can contain both abstract and concrete method. An abstract method doesn't have the body, just declaration.
4. A class automatically becomes abstract class when any of its methods declared as abstract.
5. abstract method doesn't have method body.
6. In Java, a variable can not be made abstract , its only class or methods which would be abstract.
7. If a class extends an abstract class or interface it has to provide implementation to all its abstract method to be a concrete class. alternatively, this class can also be abstract.

## References

* [javarevisited-abstraction](http://javarevisited.blogspot.com/2010/10/abstraction-in-java.html)
