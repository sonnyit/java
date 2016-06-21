---
title: Design Pattern - Decorator
updated: 2016-06-20
layout: single
categories:
  - java-design-pattern
tags:
  - java-design-pattern
---

### Tables

* [What is decorator design pattern in Java?](#what-is-decorator-design-pattern-in-java-10548tables)
* [Problem which is solved by Decorator Pattern](#problem-which-is-solved-by-decorator-pattern-10548tables)
* [When to use Decorator pattern in Java](#when-to-use-decorator-pattern-in-java-10548tables)
* [UML Diagram for Decorator Design Pattern](#uml-diagram-for-decorator-design-pattern-10548tables)
* [Code Example of decorator design pattern](#code-example-of-decorator-design-pattern-10548tables)
* [References](#references-10548tables)

## What is decorator design pattern in Java? [&#10548;](#tables)

* Decorator design pattern is used to **enhance the functionality of a particular object at run-time** or **dynamically**.
* At the same time **other instance of same class will not be affected by this** so individual object gets the new behavior.
* Basically we wrap the original object through decorator object.
* Decorator design pattern is based on abstract classes and we derive concrete implementation from that classes,
* It’s a structural design pattern and most widely used.

## Problem which is solved by Decorator Pattern [&#10548;](#tables)

If anyone wants to add some functionality to individual object or change the state of particular object at run time it is not possible. What the possible is we can provide the specific behavior to all the object of that class at design time by the help of inheritance or using subclass.

But **Decorator pattern** makes possible that we provide individual object of same class a specific behavior or state at run time. This doesn’t affect other object of same Class in Java.

## When to use Decorator pattern in Java [&#10548;](#tables)

* When sub classing is become impractical and we need large number of different possibilities to make independent object or we can say we have number of combination for an object.

* Secondly when we want to add functionality to individual object not to all object at run-time we use decorator design pattern.

## UML Diagram for Decorator Design Pattern [&#10548;](#tables)

![decorator-pattern](http://www.codeproject.com/KB/architecture/468951/DecoratorDesignPatternGeneric.gif)

* **Component:** defines interface for objects that can have additional responsibilities added to them.
* **ConcreteComponent:** defines an object on which additional responsibilities can be added
* **Decorator:** maintains a reference to component object and defines an interface that conforms to component's interface. In simple words, it has a component object to be decorated.
* **ConcreteDecorator:** add responsibilities to the component object.

## Code Example of decorator design pattern [&#10548;](#tables)

Decorator for Pizza problem:

![pizza](http://d1gjlxt8vb0knt.cloudfront.net//wp-content/uploads/pizza5.jpg)

* **Pizza** acts as our abstract component class.
* There are four concrete components namely **PeppyPaneer , FarmHouse, Margherita, ChickenFiesta**.
* **ToppingsDecorator** is our abstract decorator and **FreshTomato , Paneer, Jalapeno, Barbeque** are concrete decorators.

```java
// Java program to demonstrate Decorator pattern
 
// Abstract Pizza class (All classes extend from this)
abstract class Pizza {
  // it is an abstract pizza
	String description = "Unkknown Pizza";
	
	public String getDescription() {
		return description;
	}
	
	public abstract int getCost();
}

// The decorator class :  It extends Pizza to be
// interchangable with it topings decorator can
// also be implemented as an interface
abstract class ToppingsDecorator extends Pizza {
  public abstract String getDescription();
}

// Concrete pizza classes
class PeppyPaneer extends Pizza {
  public PeppyPaneer() { description = "PeppyPaneer"; }
	public int getCost() { return 100; }
}
class FarmHouse extends Pizza{
	public FarmHouse() { description = "FarmHouse"; }
	public int getCost() { return 200; }
}
class Margherita extends Pizza {
	public Margherita() { description = "Margherita"; }
	public int getCost() { return 100; }
}
class ChickenFiesta extends Pizza {
	public ChickenFiesta() { description = "ChickenFiesta"; }
	public int getCost() { return 200; }
}

class SimplePizza extends Pizza{
	public SimplePizza(){
		description = "SimplePizza";
	}
	
	public int getCost(){
		return 50;
	}
}

// Concrete toppings classes
class FreshTomato extends ToppingsDecorator{
	// We need a reference to obj we are decorating
	Pizza pizza;
	
	public FreshTomato(Pizza pizza) {
	  // if request to decorate null pizza make a simple one
		if(pizza != null)
			this.pizza  = pizza;
		else
			this.pizza = new SimplePizza();
	}
	
	public String getDescription(){
		return pizza.getDescription() + ", Fresh Tomato ";
	}
	
	public int getCost() { return 40 + pizza.getCost(); }
}

class Barbeque extends ToppingsDecorator {
	Pizza pizza;                  
	
	public Barbeque(Pizza pizza) {
		if(pizza != null)
			this.pizza  = pizza;
		else
			this.pizza = new SimplePizza();
	}
	
	public String getDescription() {
		return pizza.getDescription() + ", Barbeque ";
	}
	
	public int getCost(){
		return 90 + pizza.getCost();
	}
}

class Paneer extends ToppingsDecorator {
	Pizza pizza;
	
	public Paneer(Pizza pizza) {
		if(pizza != null)
			this.pizza  = pizza;
		else
			this.pizza = new SimplePizza();
	}	
	
	public String getDescription() {
		return pizza.getDescription() + ", Paneer ";
	}
	
	public int getCost() {
		return 70 + pizza.getCost();
	}
}

// Other toppings can be coded in a similar way

class PizzaStore{
	public static void main(String args[]) {
	  // create new margherita pizza
		Pizza pizza = new Margherita();
		System.out.println( pizza.getDescription() + "  Cost :" + pizza.getCost());
		
		// create new FarmHouse pizza
		Pizza pizza2 = new FarmHouse();
		
		// decorate it with freshtomato topping
		pizza2 = new FreshTomato(pizza2);
		//decorate it with paneer topping
		pizza2 = new Paneer(pizza2);
		System.out.println( pizza2.getDescription() + "  Cost :" + pizza2.getCost());
		
		Pizza pizza3 = new Barbeque(null);    //no specific pizza
		System.out.println( pizza3.getDescription() + "  Cost :" + pizza3.getCost());
	}
}
```

Output:

```bash
Margherita  Cost :100
FarmHouse, Fresh Tomato , Paneer   Cost :310
SimplePizza, Barbeque   Cost :140
```

## References [&#10548;](#tables)
* [geeksforgeeks-decorator-pattern](http://www.geeksforgeeks.org/decorator-pattern-set-3-coding-the-design/?utm_source=twitterfeed&utm_medium=twitter&utm_campaign=Feed%3A+Geeksforgeeks+%28GeeksforGeeks%29)
* [codeproject-decorator-pattern](http://www.codeproject.com/Tips/468951/Decorator-Design-Pattern-in-Java)
* [programcreek-decorator-pattern](http://www.programcreek.com/2012/05/java-design-pattern-decorator-decorate-your-girlfriend/)
* [javarevisited-decorator-pattern](http://javarevisited.blogspot.com/2011/12/factory-design-pattern-java-example.html)