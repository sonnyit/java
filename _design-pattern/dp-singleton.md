---
title: Design Pattern - Singleton
updated: 2016-06-20
layout: single
categories:
  - java-design-pattern
tags:
  - java-design-pattern
---

Singleton pattern is one of the most commonly used patterns in Java. It is used to control the number of objects created by preventing external instantiation and modification. This concept can be generalized to systems that operate more efficiently when only one object exists, or that restrict the instantiation to a certain number of objects, such as:

1. private constructor - no other class can instantiate a new object.
2. private reference - no external modification.
3. public static method is the only place that can get an object.

### Tables

* [The Story for Singleton](#the-story-for-singleton-10548tables)
* [Class Diagram and Code](#class-diagram-and-code-10548tables)
* [Singleton Pattern Used in Java Stand Library](#singleton-pattern-used-in-java-stand-library-10548tables)
* [Another Implementation of Singleton Pattern](#another-implementation-of-singleton-pattern-10548tables)
* [References](#references-10548tables)

## The Story for Singleton [&#10548;](#tables)

Here is a simple use case. A country can have only one president. So whenever a president is needed, the only president should be returned instead of creating a new one. The **getPresident()** method will make sure there is always only one president created.

## Class Diagram and Code [&#10548;](#tables)

![singleton](http://www.programcreek.com/wp-content/uploads/2011/07/singleton.jpg)

### Eager Mode:

```java
public class AmericaPresident {
	private static final AmericaPresident thePresident = new AmericaPresident();
 
	private AmericaPresident() {}
 
	public static AmericaPresident getPresident() {
		return thePresident;
	}
}
```

thePresident is declared as final, so it will always contain the same object reference.

### Lazy Mode:

```java
public class AmericaPresident {
	private static AmericaPresident thePresident;
 
	private AmericaPresident() {}
 
	public static AmericaPresident getPresident() {
		if (thePresident == null) {
			thePresident = new AmericaPresident();
		}
		return thePresident;
	}
}
```

## Singleton Pattern Used in Java Stand Library [&#10548;](#tables)

[detail](http://www.programcreek.com/2011/07/java-design-pattern-singleton/)

## Another Implementation of Singleton Pattern [&#10548;](#tables)

As private constructor doesn't protect from instantiation via reflection, Joshua Bloch (Effective Java) proposes a better implementation of Singleton. If you are not familiar with Enum, here is a good example from Oracle.

```java
public enum AmericaPresident{
	INSTANCE;
 
	public static void doSomething(){
		//do something
	}
}
```

## References [&#10548;](#tables)
* [programcreek-singleton](http://www.programcreek.com/2011/07/java-design-pattern-singleton/)