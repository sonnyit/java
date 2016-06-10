---
title: Java Abstract
updated: 2015-12-02
---

Abstraction is the concept of exposing only the required essential characteristics and behavior with respect to a context.

## Java Abstract Class
A **Java class** that is declared using the keyword **abstract** is called an **abstract class**.

New **instances cannot be created** for an **abstract class** but it can be **extended**.

An abstract class can have abstract methods and concrete methods or both. Methods with implementation body are concrete methods. But if a class have at least one abstract method, then the class **must** be declared **abstract**.

An abstract class can have *static fields* and *methods* and they can be used the same way as used in a concrete class.

To use an abstract class you have to inherit it from another class, provide implementations to the abstract methods in it.

```java
public abstract class Animal {
}
```

## Java Abstract Method
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

## Extending an Abstract Class
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

## Abstract class Implements an Interface
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

## When Should I use an Abstract class
We should go for abstract class when we are working with **classes** that **contains similar code**. That is, there is a possibility to template behavior and attributes. So, what we gain from this template pattern is avoiding repetition of common code.

Common behavior can be elevated to a super class and provide implementation to it. Then add behavior that cannot be implemented and declare it as abstract. Classes that are similar to this abstract class will extend it and use the already implemented methods and add implementation for abstract methods.

## Can an Abstract Class have Constructor in Java?
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

## Can an Abstract class be final in Java?
**No,** an abstract class cannot be declared as **final** in Java. Because it will completely negate the purpose of an abstract class.

An abstract class should be extended to create instances. If it is declared final, then it cannot be extended and so an abstract class cannot be declared as final.

##### [Java Site Map](../java-sitemap)
