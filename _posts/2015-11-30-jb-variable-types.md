---
title: Java Basic - Variable Types
updated: 2015-11-30
---

There are three kinds of variables in Java:

* Local variables
* Instance variables
* Class/static variables

## Local variables

- Local variables are declared in methods, constructors, or blocks.
- Local variables are created when the method, constructor or block is entered and the variable will be destroyed once it exits the method, constructor or block.
- Access modifiers cannot used for local variables.
- Local variables are visible only within the declared method, constructor or block.
- Local variable are implemented at **stack** level internally.
- **There are no default value for local variables** so local variables **should be declared** and **initial value** should be assigned **before the first use**.

## Instance variables

- Instance variables are declared in a class, but outside a method, constructor or any block.
- When a space is allocated for an object in the heap, a slot for each instance variable value is created.
- Instance variables are created when an object is created with the use of the keyword *'new'* and destroyed when the object is destroyed.
- Instance variables can be declared in class level before or after use.
- Access modifiers can be given for instance variables.
- The instance variables are visible for all methods, constructors and block in the class.
- Instance variables have default values. For numbers, default value is **0**. For booleans, it is **false**. And for object references it is **null**. Values can be assigned during the declaration or within the constructor.

[read more 1](http://www.tutorialspoint.com/java/java_variable_types.htm) [read more 2](http://math.hws.edu/javanotes/c5/s1.html)

## Class/static variables

- Class variables also known as static variables are declared with the **static** keyword in a class, but outside a method, constructor or block.
- There would only be one copy of each class variable per class, regardless of how many objects are created from it.
- Static variables are stored in static memory.
- Static variables are created when program starts and destroyed when the program stops.
- Visibility is similar to instance variables.
- Default values are same as instance variables. (0, false, null). Values can be assigned during the declaration or within the constructor. Additionally values can be assigned in special static initializer blocks.
- Static variables can be accessed be calling with the class name *ClassName.VariableName*.
* When declaring class variables as:
    * *public static final* --> variable names (constants) are all in upper case.
    * If *static final* but not *public* --> variable naming syntax is the same as instance and local variables.

**Example:**

```java
import java.io.*;

public class Employee{
     // salary variable is a private static variable
    private static double salary;

    // DEPARTMENT is a constant
    public static final String DEPARTMENT = "Development ";

    public static void main(String args[]){
        salary = 1000;
        System.out.println(DEPARTMENT + "average salary:" + salary);
    }
}
```

##### [Java Site Map](../java-sitemap)
