---
title: Java Basic - Exceptions
updated: 2016-06-13
layout: single
categories:
  - java-basic
tags:
  - java-basic
---

### Tables

* [What is an exception?](#what-is-an-exception-10548tables)
  * [When an exception can occur?](#when-an-exception-can-occur-10548tables)
  * [Reasons for Exceptions](#reasons-for-exceptions-10548tables)
* [Difference between error and exception](#difference-between-error-and-exception-10548tables)
  * [Why to handle exception?](#why-to-handle-exception-10548tables)
  * [Advantages of Exception Handling](#advantages-of-exception-handling-10548tables)
* [Types of exceptions](#types-of-exceptions-10548tables)
  * [Checked exceptions](#checked-exceptions-10548tables)
  * [Unchecked exceptions](#unchecked-exceptions-10548tables)
  * [Exception hierarchy](#exception-hierarchy-10548tables)
* [User defined Exception subclass](#user-defined-exception-subclass-10548tables)
  * [User custom exceptions - Points to remember](#user-custom exceptions - Points to remember)
* [try-catch - Exception handling](#try-catch---exception-handling-10548tables)
  * [What is try-catch block?](#what-is-try-catch-block-10548tables)
  * [Multiple catch](#multiple-catch-10548tables)
  * [Unreachable catch block](#unreachable-catch-block-10548tables)
  * [Nested try statement](#nested-try-statement-10548tables)
  * [What is finally block?](#what-is-finally-block-10548tables)
  * [Cases when the finally block doesn’t execute](#cases-when-the-finally-block-doesnt-execute-10548tables)
* [throw and throws in Java](#throw-and-throws-in-java-10548tables)
* [Important points to remember](#important-points-to-remember-10548tables)
* [Reference](#reference-10548tables)

## What is an exception? [&#10548;](#tables)

An Exception can be anything which interrupts the normal flow of the program. When an exception occurs program processing gets terminated and doesn’t continue further. In such cases we get a system generated error message. The good thing about exceptions is that they can be handled.

A Java Exception is an object that describes the exception that occurs in a program. When an exceptional events occurs in Java, an exception is said to be thrown. The code that 's responsible for doing something about the exception is called an exception handler.

### When an exception can occur? [&#10548;](#tables)

Exception can occur at runtime (known as runtime exceptions) as well as at compile-time (known Compile-time exceptions).

### Reasons for Exceptions [&#10548;](#tables)

There can be several reasons for an exception. For example, following situations can cause an exception: 

* Opening a non-existing file
* Network connection problem
* Operands being manipulated are out of prescribed ranges
* Class file missing which was supposed to be loaded and so on

## Difference between error and exception [&#10548;](#tables)

* **Errors** indicate serious problems and abnormal conditions that most applications should not try to handle. Error defines problems that are not expected to be caught under normal circumstances by our program. For example memory error, hardware error, JVM error etc.
* **Exceptions** are conditions within the code. A developer can handle such conditions and take necessary corrective actions. Few examples :
  * DivideByZero exception
  * NullPointerException
  * ArithmeticException
  * ArrayIndexOutOfBoundsException

### Why to handle exception? [&#10548;](#tables)

If an exception is raised, which has not been handled by programmer then program execution can get terminated and system prints a non user friendly error message.

### Advantages of Exception Handling [&#10548;](#tables)

* Exception handling allows us to control the normal flow of the program by using exception handling in program.
* It throws an exception whenever a calling method encounters an error providing that the calling method takes care of that error.
* It also gives us the scope of organizing and differentiating between different error types using a separate block of codes. This is done with the help of try-catch blocks.

## Types of exceptions [&#10548;](#tables)

There are two types of exceptions

1. **Checked exceptions**
2. **Unchecked exceptions**

### Checked exceptions [&#10548;](#tables)

Checked exceptions are checked at compile-time. It means if a method is throwing a checked exception then it should handle the exception using **try-catch block** or it should declare the exception using **throws keyword**, otherwise the program will give a compilation error. It is named as **checked exception** because these exceptions are **checked** at Compile time.

Here are the few other Checked Exceptions –

* SQLException
* IOException
* DataAccessException
* ClassNotFoundException
* InvocationTargetException
* IllegalAccessException
* NoSuchFieldException
* EOFException etc.

### Unchecked exceptions [&#10548;](#tables)

* Unchecked exceptions are not checked at compile time. It means if your program is throwing an unchecked exception and even if you didn’t handle/declare that exception, the program won’t give a compilation error. Most of the times these exception occurs due to the bad data provided by user during the user-program interaction. It is up to the programmer to judge the conditions in advance, that can cause such exceptions and handle them appropriately. All Unchecked exceptions are direct sub classes of **RuntimeException** class.
* Runtime Exceptions are also known as Unchecked Exceptions as the compiler do not check whether the programmer has handled them or not but it’s the duty of the programmer to handle these exceptions and provide a safe exit.
* These exceptions need not be included in any method’s throws list because compiler does not check to see if a method handles or throws these exceptions.

Here are the few most frequently seen unchecked exceptions –

* NullPointerException
* ArrayIndexOutOfBoundsException
* ArithmeticException
* IllegalArgumentException
* NegativeArraySizeException etc.

### Exception hierarchy [&#10548;](#tables)

![exception-hierarchy](http://beginnersbook.com/wp-content/uploads/2013/04/Exception-classes-Hierarchy.png)

## User defined Exception subclass

You can also create your own exception sub class simply by extending java **Exception** class. You can define a constructor for your Exception sub class (not compulsory) and you can override the **toString()** function to display your customized message on catch.

```java
class MyException extends Exception {
 private int ex;
 MyException(int a) {
  ex=a;
 }
 public String toString() {
  return "MyException[" + ex +"] is less than zero";
 }
}

class Test {
 static void sum(int a,int b) throws MyException {
  if(a<0) {
   throw new MyException(a);
  }
  else { 
   System.out.println(a+b); 
  }
 }

 public static void main(String[] args) {
  try {
   sum(-10, 10);
  }
  catch(MyException me) {
   System.out.println(me);
  }
 }
}
```

### User custom exceptions - Points to remember

1. Extend the Exception class to create your own ecxeption class.
2. You don't have to implement anything inside it, no methods are required.
3. You can have a Constructor if you want.
4. You can override the toString() function, to display customized message.

## try-catch - Exception handling [&#10548;](#tables)

Exception Handling is the mechanism to handle runtime malfunctions. We need to handle such exceptions to prevent abrupt termination of program.

### What is try-catch block? [&#10548;](#tables)

* The try block contains a block of program statements within which an exception might occur. A try block is always followed by a catch block, which handles the exception that occurs in associated try block.
* The corresponding catch block executes if an exception of a particular type occurs within the try block.
* A try block must followed by a catch block or finally block or both.

#### Syntax of try-catch in Java

```java
try
{
     //statements that may cause an exception
}
catch (exception(type) e(object))‏
{
     //error handling code
}
```

### Multiple catch [&#10548;](#tables)

* A try block can be followed by multiple catch blocks.
* You can add any number of catch blocks after a single try block. If an exception occurs in the guarded code, the exception is passed to the first catch block in the list.
* If the exception type of exception, matches with the first catch block it gets caught. If not, the exception is passed down to the next catch block.
* This continue until the exception is caught or falls through all catches (will shows a system generated message)

### Unreachable catch block [&#10548;](#tables)

While using multiple catch statements, it is important to remember that: exception subclasses inside catch must come before any of their super classes, otherwise it will lead to compile time error.

### Nested try statement [&#10548;](#tables)

* try statement can be nested inside another block of try.
* Nested try block is used when a part of a block may cause one error while entire block may cause another error.
* In case if inner try block does not have a catch handler for a particular exception then the outer try is checked for match.

### What is finally block? [&#10548;](#tables)

* A **finally statement** must be associated with a **try statement**. It identifies a block of statements that needs to be executed **regardless of whether or not** an exception occurs within the try block.
* In normal execution the finally block is executed after try block. When any exception occurs first the catch block is executed and then finally block is executed.
* An exception in the finally block, exactly **behaves like any other exception**.
* The code present in the **finally block** executes even if the try or catch block contains control transfer statements like **return, break or continue**.

#### Syntax of finally block

```java
try
{
    //statements that may cause an exception
}
finally
{
   //statements to be executed
}
```

### Cases when the finally block doesn’t execute [&#10548;](#tables)

The circumstances that prevent execution of the code in a finally block are:

* The death of a Thread
* Using of the System.exit() method.
* Due to an exception arising in the finally block.

## throw and throws in Java [&#10548;](#tables)

1. **throws clause** in used to declare an exception and **throw** keyword is used to throw an exception explicitly.
2. If we see syntax, **throw** is followed by an instance variable and **throws** is followed by exception class names.
3. The keyword **throw** is used inside method body to invoke an exception and **throws clause** is used in method declaration (signature).
4. By using **throw** keyword in java, you cannot throw more than one exception but using **throws** you can declare multiple exceptions.

## Important points to remember [&#10548;](#tables)

1. If you do not explicitly use the try catch blocks in your program, Java will provide a default exception handler, which will print the exception details on the terminal, whenever exception occurs.
2. Super class Throwable overrides toString() function, to display error message in form of string.
3. While using multiple catch block, always make sure that exception subclasses come before any of their super class. Else you will get compile time error (unreachable ...)
4. In nested try catch, the inner try block, uses its own catch block as well as catch block of the outer try, if required.
5. Only the object of Throwable class or its subclasses can be thrown.
6. A try block must followed by a catch block **or** finally block **or** both.
7. The code present in the **finally block** executes even if the try or catch block contains control transfer statements like **return, break or continue**.

## Reference [&#10548;](#tables)
* [beginnersbook-exception-handling](http://beginnersbook.com/2013/04/java-exception-handling/)
* [beginnersbook-checked-unchecked-exceptions](http://beginnersbook.com/2013/04/java-checked-unchecked-exceptions-with-examples/)
* [beginnersbook-try-catch](http://beginnersbook.com/2013/04/try-catch-in-java/)