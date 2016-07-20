---
title: Java Basic - Basic DataTypes
updated: 2015-12-01
layout: single
categories:
  - java-basic
tags:
  - java-basic
---

There are two data types available in Java:

* Primitive Data Types: numeric types, boolean type, and returnAddress type.
* Reference/Object Data Types

### Tables

* [Primitive Data Types](#primitive-data-types-10548tables)
* [Reference Data Types](#reference-data-types-10548tables)
* [Java literals](#java-literals-10548tables)

## Primitive Data Types [&#10548;](#tables)
There are eight primitive data types supported by Java.

Primitives always have a value, they can never be null.

If a primitive type is not set to a value when a variable is defined, it takes a default value. For boolean values, this is false. For the others, this is a representation of zero, such as 0 for ints or 0.0f for floats.

Primitive types are the basic building blocks of Java types. They are assembled into reference types. Reference types can have methods and be assigned to null. In addition to “normal” numbers, numeric literals are allowed to begin with 0 (octal), 0x (hex), 0X (hex), 0b (binary), or 0B (binary). Numeric literals are also allowed to contain underscores as long as they are directly between two other numbers.

**Numeric Types**

* byte
  * 8 bit signed
  * minimum value is -128 (-2^7)
  * maximum value is 127 (2^7-1)
  * default value is 0
  * byte data type is used to save space in large arrays, mainly in place of integers, since a byte is four times smaller than an int.
* short
  * 16 bit signed
  * minimum value is -32768
  * maximum value is 32767
  * short data type can also be used to save memory as byte data type. A short is 2 times smaller than int.
  * default value is 0 
* int
  * 32 bit signed
  * minimum value is -2,147,483,648
  * maximum value is 2,147483,647
  * Int is generally used as the default data type for integer values unless there is a concern about memory.
  * The default value is 0
* long
  * 64 bit signed
  * minimum value is -2^63
  * maximum value is 2^63-1
  * this type is used when a wider range than int is needed
  * default value is 0L
* char
  * 16 bit unicode character (unsigned)
  * minimum value is ‘\u0000’ (or 0)
  * maximum value is ‘\uffff’ (or 65,535)
  * char data type is used to store any character

**Floating-point Primitives**

* float
  * 32 bit floating point
  * default value is 0.0F
* double
  * 64 bit floating point
  * default value is 0.0D

**Boolean type Primitive**

* boolean
  * one bit
  * there are only two possible values: true and false.
  * default value is false 

## Reference Data Types [&#10548;](#tables)

* Reference variables are created using defined constructors of the classes. They are used to access objects. These variables are declared to be of a specific type that cannot be changed.
* Class objects, and various type of array variables come under reference data type.
* Default value of any reference variable is null.
* A reference variable can be used to refer to any object of the declared type or any compatible type.
* Example: Animal animal = new Animal("giraffe");

## Java literals [&#10548;](#tables)
A literal is a source code representation of a fixed value. They are represented directly in the code without any computation.
