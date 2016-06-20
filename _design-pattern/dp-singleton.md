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