---
title: Java Inner Classes
updated: 2016-07-20
layout: single
categories:
  - java-basic
tags:
  - java-basic
---

### Tables

* [Nested classes](#nested-classes-10548tables)
* [Syntax](#syntax-10548tables)
* [Inner Classes (Non-static Nested Classes)](#inner-classes-non-static-nested-classes-10548tables)
	* [Member Inner Class](#member-inner-class-10548tables)
	* [Method-local Inner Class](#method-local-inner-class-10548tables)
	* [Anonymous Inner Class](#anonymous-inner-class-10548tables)
* [Static Nested Class](#static-nested-class-10548tables)
* [References](#references-10548tables)

## Nested classes [&#10548;](#tables)

In Java, just like methods, variables of a class too can have another class as its member. Writing a class within another is allowed in Java. The class written within is called the **nested class**, and the class that holds the inner class is called the **outer class**.

## Syntax [&#10548;](#tables)

The syntax to write a nested class is given below. Here the class Outer_Demo is the outer class and the class Inner_Demo is the nested class.

```java
class Outer_Demo{
   class Nested_Demo{   
   }   
}
```

Nested classes are divided into two types:

1. **Non-static nested classes:** These are the non-static members of a class.
2. **Static nested classes:** These are the static members of a class.

![inner_classes](http://www.tutorialspoint.com/java/images/inner_classes.jpg)

## Inner Classes (Non-static Nested Classes) [&#10548;](#tables)

Inner classes are a security mechanism in Java. We know a class cannot be associated with the access modifier private, but if we have the class as a member of other class, then the inner class can be made private. And this is also used to access the private members of a class.

Inner classes are of three types depending on how and where you define them. They are:

1. Member Inner Class
2. Method-local Inner Classlass
3. Anonymous Inner Class

### Member Inner Class [&#10548;](#tables)

Creating an inner class is quite simple, just need to write a class within a class.

Unlike a class, an inner class can be private and once you declare an inner class private, it cannot be accessed from an object outside the class.

Given below is the program to create an inner class and access it. In the given example, we make the inner class private and access the class through a method.

```java
class Outer_Demo{
   int num;
   //inner class
   private class Inner_Demo{
      public void print(){	   
         System.out.println("This is an inner class");
      }
   }
   //Accessing he inner class from the method within
   void display_Inner(){
      Inner_Demo inner = new Inner_Demo();
      inner.print();
   }
}
   
public class My_class{
   public static void main(String args[]){
      //Instantiating the outer class 
      Outer_Demo outer = new Outer_Demo();
      //Accessing the display_Inner() method.
      outer.display_Inner();
   }
}
```

Output:

```bash
This is an inner class.
```

#### Accessing the Private members [&#10548;](#tables)

Inner classes are also used to access the private members of a class.

```java
class Outer_Demo {
   //private variable of the outer class
   private int num= 175;  
   //inner class   
   public class Inner_Demo{
      public int getNum(){
         System.out.println("This is the getnum method of the inner class");
         return num;
      }
   }
}

public class My_class2{
   public static void main(String args[]){
      //Instantiating the outer class
      Outer_Demo outer=new Outer_Demo();
      //Instantiating the inner class
      Outer_Demo.Inner_Demo inner=outer.new Inner_Demo();
      System.out.println(inner.getNum());
   }
}
```

Output: 

```bash
The value of num in the class Test is: 175
```

### Method-local Inner Class [&#10548;](#tables)

In Java, we can write a class within a method and this will be a local type. Like local variables, the scope of the inner class is restricted within the method.

A method-local inner class can be instantiated only within the method where the inner class is defined. The following program shows how to use a method-local inner class.

```java
public class Outerclass{
   
   //instance method of the outer class 
   void my_Method(){
      int num = 23;
   
      //method-local inner class
      class MethodInner_Demo{
         public void print(){
            System.out.println("This is method inner class "+num);	   
         }   
      }//end of inner class
	   
      //Accessing the inner class
      MethodInner_Demo inner = new MethodInner_Demo();
      inner.print();
   }
   
   public static void main(String args[]){
      Outerclass outer = new Outerclass();
      outer.my_Method();	   	   
   }
}
```

Output:

```bash
This is method inner class 23
```

### Anonymous Inner Class [&#10548;](#tables)

An inner class declared without a class name is known as an anonymous inner class. In case of anonymous inner classes, we declare and instantiate them at the same time. Generally they are used whenever you need to override the method of a class or an interface. The syntax of an anonymous inner class is as follows:

```java
AnonymousInner an_inner = new AnonymousInner(){
   public void my_method(){
   ........
   ........
   }	    
};
```

The following program shows how to override the method of a class using anonymous inner class.

```java
abstract class AnonymousInner{
   public abstract void mymethod();
}

public class Outer_class {
   public static void main(String args[]){
      AnonymousInner inner = new AnonymousInner(){
         public void mymethod(){
            System.out.println("This is an example of anonymous inner class");    	  
         }	    
      };
      inner.mymethod();	
   }
}
```

If you compile and execute the above program, you will get the following result.

```bash
This is an example of anonymous inner class
```

In the same way, you can override the methods of the concrete class as well as the interface using an anonymous inner class.

### Anonymous Inner Class as Argument [&#10548;](#tables)

```java
//interface
interface Message{
   String greet();	
}

public class My_class {
   //method which accepts the object of interface Message
   public void displayMessage(Message m){
      System.out.println(m.greet() +", This is an example of anonymous inner class as an argument");	   
   }

   public static void main(String args[]){
      //Instantiating the class
      My_class obj = new My_class();
		
      //Passing an anonymous inner class as an argument
      obj.displayMessage(new Message(){
         public String greet(){
            return "Hello";  		   
         }
      });
   }
}
```

Output:

```bash
Hello This is an example of anonymous inner class as an argument
```

## Static Nested Class [&#10548;](#tables)

A static inner class is a nested class which is a static member of the outer class. It can be accessed without instantiating the outer class, using other static members. Just like static members, a static nested class does not have access to the instance variables and methods of the outer class. The syntax of static nested class is as follows:

```java
class MyOuter {
   static class Nested_Demo{
   }
}
```

Instantiating a static nested class is a bit different from instantiating an inner class. The following program shows how to use a static nested class.

```java
public class Outer{
   static class Nested_Demo{
      public void my_method(){
         System.out.println("This is my nested class");
      }
   }
   
   public static void main(String args[]){
      Outer.Nested_Demo nested = new Outer.Nested_Demo();	 
      nested.my_method();
   }
   
}
```

Output:

```bash
This is my nested class
```

## References [&#10548;](#tables)
* [tutorialspoint-innerclasses](http://www.tutorialspoint.com/java/java_innerclasses.htm)