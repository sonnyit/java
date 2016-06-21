---
title: Design Pattern - Builder
updated: 2016-06-20
layout: single
categories:
  - java-design-pattern
tags:
  - java-design-pattern
---

The key feature of Builder pattern is that it involves a step-by-step process to build something, i.e., every produce will follow the same process even though each step is different.

### Tables

* [What problem Builder pattern solves in Java](#what-problem-builder-pattern-solves-in-java-10548tables)
* [Guidelines for Builder design pattern in Java](#guidelines-for-builder-design-pattern-in-java-10548tables)
* [Advantages and Disadvantages of Builder pattern](#advantages-and-disadvantages-of-builder-pattern-10548tables)
* [When to use Builder Design pattern in Java](#when-to-use-builder-design-pattern-in-java-10548tables)
* [References](#references-10548tables)

## What problem Builder pattern solves in Java [&#10548;](#tables)

**Builder** pattern is a **creational** design pattern it means its solves problem related to object creation.

Constructors in Java are used to create object and can take parameters required to create object.

Problem starts when an Object can be created with **lot of parameters**, some of them may be **mandatory** and others may be optional.

Consider a class which is used to create *Cake*, now you need number of item like *egg, milk, flour* to create cake. Many of them are mandatory and some  of them are optional like *cherry, fruits* etc. If we are going to have overloaded constructor for different kind of cake then there will be many constructor and even worst they will accept many parameter.

Problems:

* too many constructors to maintain.
* error prone because many fields has same type e.g. sugar and and butter are in cups so instead of 2 cup sugar if you pass 2 cup butter, your compiler will not complain but will get a buttery cake with almost no sugar with high cost of wasting butter.

## Guidelines for Builder design pattern in Java [&#10548;](#tables)

1. Make a static nested class called *Builder* inside the class whose object will be build by Builder. In this example its *Cake*.
2. Builder class will have exactly same set of fields as original class.
3. Builder class will expose method for adding ingredients e.g. *sugar()* in this example. each method will return same *Builder* object. Builder will be enriched with each method call.
4. *Builder.build()* method will copy all builder field values into actual class and return object of *Item* class.
5. Item class (class for which we are creating Builder) should have **private constructor** to create its object from *build()* method and prevent outsider to access its constructor.

```java
public class BuilderPatternExample {
    public static void main(String args[]) {
        // Creating object using Builder pattern in java
        Cake whiteCake = new Cake.Builder().sugar(1).butter(0.5).eggs(2).vanila(2).flour(1.5).bakingpowder(0.75).milk(0.5).build();
      
        // Cake is ready to eat :)
        System.out.println(whiteCake);
    }
}

class Cake {
    private final double sugar;         //cup
    private final double butter;        //cup
    private final int eggs;
    private final int vanila;           //spoon
    private final double flour;         //cup
    private final double bakingpowder;  //spoon
    private final double milk;          //cup
    private final int cherry;

    public static class Builder {

        private double sugar;           //cup
        private double butter;          //cup
        private int eggs;
        private int vanila;             //spoon
        private double flour;           //cup
        private double bakingpowder;    //spoon
        private double milk;            //cup
        private int cherry;

        // builder methods for setting property
        public Builder sugar(double cup)  { this.sugar = cup; return this; }
        public Builder butter(double cup) { this.butter = cup; return this; }
        public Builder eggs(int number)   { this.eggs = number; return this; }
        public Builder vanila(int spoon)  { this.vanila = spoon; return this; }
        public Builder flour(double cup)  { this.flour = cup; return this; }
        public Builder bakingpowder(double spoon) { this.sugar = spoon; return this; }
        public Builder milk(double cup)   { this.milk = cup; return this; }
        public Builder cherry(int number) { this.cherry = number; return this; }
      
        // return fully build object
        public Cake build() {
            return new Cake(this);
        }
    }

    // private constructor to enforce object creation through builder
    private Cake(Builder builder) {
        this.sugar        = builder.sugar;
        this.butter       = builder.butter;
        this.eggs         = builder.eggs;
        this.vanila       = builder.vanila;
        this.flour        = builder.flour;
        this.bakingpowder = builder.bakingpowder;
        this.milk         = builder.milk;
        this.cherry       = builder.cherry;       
    }

    @Override
    public String toString() {
        return "Cake{" + "sugar=" + sugar + ", butter=" + butter + ", eggs=" + eggs + ", vanila=" + vanila + ", flour=" + flour + ", bakingpowder=" + bakingpowder + ", milk=" + milk + ", cherry=" + cherry + '}';
    } 
}
```

Output:

```bash
Cake{sugar=0.75, butter=0.5, eggs=2, vanila=2, flour=1.5, bakingpowder=0.0, milk=0.5, cherry=0}
```

## Advantages and Disadvantages of Builder pattern [&#10548;](#tables)

### Advantages

* more maintainable if number of fields required to create object is more than 4 or 5.
* less error-prone as user will know what they are passing because of explicit method call.
* more robust as only fully constructed object will be available to client.

### Disadvantages

* verbose and code duplication as Builder needs to copy all fields from Original or Item class.

## When to use Builder Design pattern in Java [&#10548;](#tables)

* **Builder Design pattern** is a creational pattern and should be used when number of parameter required in constructor is more than manageable usually 4 or at most 5.
* Don't confuse **Builder** with **Factory** pattern. There is an obvious difference between Builder and Factory pattern, as Factory can be used to create different implementation of same interface but Builder is tied up with its Container class and only returns object of Outer class.

## References [&#10548;](#tables)

* [javarevisited-builder-design-pattern](http://javarevisited.blogspot.com/2012/06/builder-design-pattern-in-java-example.html)
