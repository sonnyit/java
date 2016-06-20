---
title: Java Collections - Collections Hierarchy Diagram
updated: 2016-06-20
layout: single
categories:
  - java-collections
tags:
  - java-collections
---

### Tables

* [Collection vs. Collections](#collection-vs-collections-10548tables)
* [Class hierarchy of Collection](#class-hierarchy-of-collection-10548tables)
  * [Class hierarchy of Map](#class-hierarchy-of-map-10548tables)
* [Collection Classes Summary Table](#collection-classes-summary-table-10548tables)
* [Code Example](#code-example-10548tables)
* [References](#references-10548tables)

## Collection vs. Collections [&#10548;](#tables)

First of all, "Collection" and "Collections" are two different concepts. As you will see from the hierarchy diagram below: 

* "Collection" is a root interface in the Collection hierarchy.
* but "Collections" is a class which provide static methods to manipulate on some Collection types.

![collection-vs-collections](http://www.programcreek.com/wp-content/uploads/2009/02/CollectionVsCollections.jpeg)

## Class hierarchy of Collection [&#10548;](#tables)

![class-hierarchy-collection](http://www.programcreek.com/wp-content/uploads/2009/02/java-collection-hierarchy.jpeg)

### Class hierarchy of Map [&#10548;](#tables)

![class-hierarchy-map](http://www.programcreek.com/wp-content/uploads/2009/02/MapClassHierarchy-600x354.jpg)

## Collection Classes Summary Table [&#10548;](#tables)

![collection-classes-table](http://www.programcreek.com/wp-content/uploads/2009/02/collection.bmp)

## Code Example [&#10548;](#tables)

```java
List<String> a1 = new ArrayList<String>();
a1.add("Program");
a1.add("Creek");
a1.add("Java");
a1.add("Java");
System.out.println("ArrayList Elements");
System.out.print("\t" + a1 + "\n");
 
List<String> l1 = new LinkedList<String>();
l1.add("Program");
l1.add("Creek");
l1.add("Java");
l1.add("Java");
System.out.println("LinkedList Elements");
System.out.print("\t" + l1 + "\n");
 
Set<String> s1 = new HashSet<String>(); // or new TreeSet() will order the elements;
s1.add("Program");
s1.add("Creek");
s1.add("Java");
s1.add("Java");
s1.add("tutorial");
System.out.println("Set Elements");
System.out.print("\t" + s1 + "\n");
 
Map<String, String> m1 = new HashMap<String, String>(); // or new TreeMap() will order based on keys
m1.put("Windows", "2000");
m1.put("Windows", "XP");
m1.put("Language", "Java");
m1.put("Website", "programcreek.com");
System.out.println("Map Elements");
System.out.print("\t" + m1);
```

## References [&#10548;](#tables)

* [programcreek-class-hierarchy-for-collections](http://www.programcreek.com/2009/02/the-interface-and-class-hierarchy-for-collections/)
* [programcreek-collection-classes-summary](http://www.programcreek.com/2009/02/collection-interface-concrete-implementation-classes-summary-and-some-examples/)
* [programcreek-java-collections](http://www.programcreek.com/java-collections/)
* [programcreek-java-collections-questions](http://www.programcreek.com/2013/09/top-10-questions-for-java-collections/)