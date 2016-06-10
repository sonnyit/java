---
title: Java Basic - Static and Final Keyword
updated: 2015-12-01
categories:
  - java
---

## Java Static

### Java Static Variables

* Java instance variables are given separate memory for storage. If there is a need for a variable to be common to all the objects of a single Java class, then the static modifier should be used in the variable declaration.
* Any Java object that belongs to that class can modify its static variables.
* Also, an instance is not a must to modify the static variable and it can be accessed using the Java class directly.
* Static variables can be accessed by java instance methods also.
* When the value of a constant is known a compile time it is declared 'final' using the 'static' keyword.

### Java Static Methods

* Similar to static variables, java static methods are also common to classes and not tied to a java instance.
* Good practice in java is that, static methods should be invoked with using the class name though it can be invoked using an object.
ClassName.methodName(arguments) or 
objectName.methodName(arguments).
* General use for java static methods is to access static fields.
* Static methods can be accessed by java instance methods.
* Java static methods cannot access instance variables or instance methods directly.
* Java static methods cannot use the *this* keyword.

### Java Static Class

* For java classes, only an *inner class* can be declared using the static modifier. That basically helps you to use the *nested/inner* class without creating an instance of the outer class.
* For java a static inner class it does not mean that, all their members are static. These are called nested static classes in java.

## Java Static Import
[read here](http://javapapers.com/core-java/what-is-a-static-import-in-java/)

## Java Final Keyword

* A java variable can be declared using the keyword **final**. Then the final variable can be assigned only once.
* A variable that is declared as final and not initialized is called a blank final variable. A blank final variable forces the constructors to initialize it.
* Java **classes** declared as **final cannot be extended**. Restricting inheritance!
* **Methods** declared as **final cannot be overridden**. In methods private is equal to final, but in variable it is not.
* final parameters - values of the parameters cannot be changed after initialization. 
* Java local classes can only reference local variables an parameters, that are declared as final.
* A visible advantage of declaring a java variable as static final is, the compiled java class results in faster performance.

### More discussion:

* *final* should not be called as constants. Because when an array is declared as final, the state of the object stored in the array can be modified. You need to make it immutable in order not to allow modifications. In general context constants will not allow to modify. In C++, an array declared as const will not allow the above scenario but java allows. So java's final is not the general constant used across in computer languages.
* A variable is declared as static final is closed to constants in general software terminology. You must instantiate the variable when you declare it static final.

##### [Java Site Map](../java-sitemap)
