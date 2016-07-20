---
title: Java Basic - Modifier Types
updated: 2015-12-01
categories:
  - java-basic
tags:
  - java-basic
---

**Modifiers** are **keywords** that you **add to those definitions** to **change their meanings**. In Java language, we have:

* Java Access Modifiers
* Non Access Modifiers

To use a modifier, we include its **keyword** in the definition of a class, method, or variable.

### Tables

* [Java Access Control Modifiers](#java-access-control-modifiers-10548tables)
	* [Access Modifiers for Top-level Classes & Interfaces](#access-modifiers-for-top-level-classes--interfaces-10548tables)
	* [Accessibility Modifiers for Members](#accessibility-modifiers-for-members-10548tables)
	* [Access Control and Inheritance](#access-control-and-inheritance-10548tables)
* [Non Access Modifiers](#non-access-modifiers-10548tables)
	* [static](#static-10548tables)
	* [abstract](#abstract-10548tables)
	* [final](#final-10548tables)
	* [synchronized (methods)](#synchronized-methods-10548tables)
	* [transient (fields)](#transient-fields-10548tables)
	* [native (methods)](#native-methods-10548tables)
	* [volatile (fields)](#volatile-fields-10548tables)

## Java Access Control Modifiers [&#10548;](#tables)

Access Modifiers are used at 2 access levels in Java. They are

1. Top-level for Classes & Interfaces
2. Member-level for Classes & Interfaces

### Access Modifiers for Top-level Classes & Interfaces [&#10548;](#tables)

Only 2 basic access modifiers are applicable for Top-level Classes & Interfaces. They are **Public** and **Package/Default** modifiers.

* **Public:**  if top level class or interface within a package is declared as Public, then it is accessible both inside and outside of the package.
* **Default:** If no access modifier is specified in the declaration of the top level class or interface, then it is accessible only within package level. It is not accessible in other packages or sub packages.

### Accessibility Modifiers for Members [&#10548;](#tables)

* **default (no modifier)** 
	* Available to any other class in the same package.
	* The fields in an interface are implicitly public static final and the methods in an interface are by default public.
* **private**
	* Methods, Variables and Constructors that are declared private can only be accessed within the declared class itself.
	* Private access modifier is the most restrictive access level. **Class and interfaces cannot be private**. Marking a class with the private access modifier would mean that no other class could access it, which means that you could not really use the class at all. Therefore the private access modifier is not allowed for classes.
	* Variables that are declared private can be accessed outside the class if public getter methods are present in the class.
	* Using the private modifier is the main way that an object encapsulates itself and hide data from the outside world.
	* If a constructor in a class is assigned the private Java access modifier, that means that the constructor cannot be called from anywhere outside the class. A private constructor can still get called from other constructors, or from static methods in the same class.
* **public**
	* A class, method, constructor, interface etc declared public can be accessed from any other class. Therefore fields, methods, blocks declared inside a public class can be accessed from any class belonging to the Java Universe.
	* However if the public class we are trying to access is in a different package, then the public class still need to be imported.
	* Because of class inheritance, all public methods and variables of a class are inherited by its subclasses.
* **protected**
	* Variables, methods and constructors which are declared protected in a superclass can be accessed only by the subclasses even if in other package or any class within the package of the protected members' class.
	* The protected access modifier cannot be applied to class and interfaces. Methods, fields can be declared protected, however methods and fields in a interface cannot be declared protected.
	* Protected access gives the subclass a chance to use the helper method or variable, while preventing a nonrelated class from trying to use it.

| Access Modifiers | Same Class | Same Package | Sub Class | Other Package |
| ---------------- | ---------- | ------------ | --------- | ------------- |
| public  | Y | Y | Y | Y |
| protected | Y | Y | Y | N |
| no access modifier | Y | Y | N | N |
| private | Y | N | N | N |

**Note:** It is important to keep in mind that the Java access modifier assigned to a Java class takes precedence over any access modifiers assigned to fields, constructors and methods of that class. If the class is marked with the default access modifier, then no other class outside the same Java package can access that class, including its constructors, fields and methods. It doesn't help that you declare these fields public, or even public static.

### Access Control and Inheritance [&#10548;](#tables)

When you create a subclass of some class, the methods in the subclass cannot have less accessible access modifiers assigned to them than they had in the superclass.

* Methods declared **public** in a superclass also must be **public** in all subclasses.
* Methods declared **protected** in a superclass must either be **protected** or **public** in subclasses; they cannot be private.
* Methods declared **private** are **not inherited** at all, so there is no rule for them.

While it is not allowed to decrease accessibility of an overridden method, it is allowed to expand accessibility of an overridden method.

* Methods declared **default** in a superclass is allowed to assign **public** access in all subclasses.

## Non Access Modifiers [&#10548;](#tables)
Java provides a number of non-access modifiers to achieve many other functionality.

1. static
2. abstract
3. final
4. synchronized
5. transient
6. native
7. volatile

* The **synchronized** and **volatile** modifiers, which are use for threads.

### static [&#10548;](#tables)

* The **static** modifier for creating class methods and variables.

### abstract [&#10548;](#tables)

- Java does not have abstract variable.
- If method has a keyword **abstract** in its declaration, then such method/function is called Abstract method.
- Abstract methods does not have an implementation (method body is not defined); only method prototype is specified in the class definition.

* **Note:**
	* Only instance methods can be declared as abstract.
	* Since static methods cannot be overridden, so declaring abstract static method would of no use.
	* A Final method cannot be abstract and vice versa.
	* Methods specified in an Interface are implicitly abstract.

### final [&#10548;](#tables)

* The **final** modifier for finalizing the implementations of classes, methods and variables.

### synchronized (methods) [&#10548;](#tables)

* Multiple threads can be executing in a program and at times they might try to execute several methods on the same object simultaneously.
* If there is a requirement that only one thread at a time should execute a method in the object, then such methods can be declared as **synchronized**. Their execution will be mutually exclusive among all threads. At any given time, at the most one thread will be executing a synchronized method on an object.

* **Note:** Synchronized methods are also applicable to Static methods of a class.

### transient (fields) [&#10548;](#tables)

* Objects can be stored using serialization. Serialization transforms objects into an output format which is helpful for storing objects. Objects can later be retrieved in the same state as when they were serialized, meaning that fields included in the serialization will have the same values at the time of serialization. Such objects are said to be Persistent.
* The fields are declared with keyword Transient in their class declaration if its value should not be saved when objects of the class are written to persistent storage.

```java
class sample implements Serializable {
   transient str varStr; // transient field declaration
   int varInt; // instance field declaration
}
```

### native (methods) [&#10548;](#tables)

* Native Methods are also called as Foreign methods. Such methods implementation is not defined in Java but in another programming language.
* These methods are specified in the class as method prototypes with prefix with keyword native, no method body is defined in the Java class.

```java
class cNat() {
   native void fNat(); // native method declaration
   synchronized public void fSyn() {…}; // synchronized method declaration
}
class cmain {
   public static void main (String[] args) {
     cNat cNatObj =new cNat(); // class instance creation
     cNatObj.fNAt(); // accessing native method
   }
}
```

### volatile (fields) [&#10548;](#tables)

* During execution, complied code might cache the values of fields for efficiency reasons. And as multiple threads will access the same field, caching is not allowed to cause inconsistencies when reading and writing the value in the field.
* The Volatile modifier can be used to inform the compiler that it should not attempt to perform optimizations on the field which could cause unpredicted results when the field is accessed by multiple threads

```java
class sample {
   volatile int varInt; // volatile field declaration
}
```

## References [&#10548;](#tables)
* [beginnersbook-access-modifiers](http://beginnersbook.com/2013/05/java-access-modifiers/)
* [tutorialspoint-access-modifiers](http://www.tutorialspoint.com/java/java_access_modifiers.htm)