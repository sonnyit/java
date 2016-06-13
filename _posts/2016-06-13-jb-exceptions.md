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
* [Reference](#reference-10548tables)

## What is an exception? [&#10548;](#tables)

An Exception can be anything which interrupts the normal flow of the program. When an exception occurs program processing gets terminated and doesn’t continue further. In such cases we get a system generated error message. The good thing about exceptions is that they can be handled.

### When an exception can occur? [&#10548;](#tables)

Exception can occur at runtime (known as runtime exceptions) as well as at compile-time (known Compile-time exceptions).

### Reasons for Exceptions [&#10548;](#tables)

There can be several reasons for an exception. For example, following situations can cause an exception: 

* Opening a non-existing file
* Network connection problem
* Operands being manipulated are out of prescribed ranges
* Class file missing which was supposed to be loaded and so on.
* ...

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

### Unchecked exceptions [&#10548;](#tables)

Unchecked exceptions are not checked at compile time. It means if your program is throwing an unchecked exception and even if you didn’t handle/declare that exception, the program won’t give a compilation error. Most of the times these exception occurs due to the bad data provided by user during the user-program interaction. It is up to the programmer to judge the conditions in advance, that can cause such exceptions and handle them appropriately. All Unchecked exceptions are direct sub classes of **RuntimeException** class.

Here are the few most frequently seen unchecked exceptions –

* NullPointerException
* ArrayIndexOutOfBoundsException
* ArithmeticException
* IllegalArgumentException

## Reference [&#10548;](#tables)
* [http://beginnersbook.com/2013/04/java-exception-handling/]
* [http://beginnersbook.com/2013/04/java-checked-unchecked-exceptions-with-examples/]
* [http://beginnersbook.com/2013/04/try-catch-in-java/]