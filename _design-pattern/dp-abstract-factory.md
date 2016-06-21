---
title: Design Pattern - Abstract Factory
updated: 2016-06-21
layout: single
categories:
  - java-design-pattern
tags:
  - java-design-pattern
---

**Abstract Factory** pattern adds another layer of abstraction for Factory pattern. If we compare Abstract Factory with Factory, it is pretty obvious that a new layer of abstraction is added.

Abstract Factory is a super-factory which creates other factories. We can call it "Factory of factories".

### Tables

* [Abstract Factory class diagram](#abstract-factory-class-diagram-10548tables)
* [Abstract Factory Java code](#abstract-factory-java-code-10548tables)
* [Difference between Factory and Abstract Factory pattern](#difference-between-factory-and-abstract-factory-pattern-10548tables)
* [Real use example](#real-use-example-10548tables)
* [References](#references-10548tables)

## Abstract Factory class diagram [&#10548;](#tables)

![abstract-factory](http://www.programcreek.com/wp-content/uploads/2013/02/abstract-factory-design-pattern.png)

## Abstract Factory Java code [&#10548;](#tables)

```java
interface CPU {
    void process();
}
 
interface CPUFactory {
	CPU produceCPU();
}
 
class AMDFactory implements CPUFactory {
    public CPU produceCPU() {
        return new AMDCPU();
    }
}
 
class IntelFactory implements CPUFactory {
    public CPU produceCPU() {
        return new IntelCPU();
    }
}
 
class AMDCPU implements CPU {
    public void process() {
        System.out.println("AMD is processing...");
    }
}
 
class IntelCPU implements CPU {
    public void process() {
        System.out.println("Intel is processing...");
    }
}
 
class Computer {
	CPU cpu;
 
    public Computer(CPUFactory factory) {
    	cpu = factory.produceCPU();
        cpu.process();
    }
}
 
public class Client {
    public static void main(String[] args) {
        new Computer(createSpecificFactory());
    }
 
    public static CPUFactory createSpecificFactory() {
        int sys = 0; // based on specific requirement
        if (sys == 0) 
        	return new AMDFactory();
        else 
        	return new IntelFactory();
    }
}
```

## Difference between Factory and Abstract Factory pattern

In short,

* *Abstract Factory* design pattern creates *Factory*
* *Factory* design pattern creates *Products*

## Real use example [&#10548;](#tables)

Actually, this is a very important concept of modern frameworks. [Here](http://stackoverflow.com/questions/1993397/abstract-factory-pattern-on-top-of-ioc/1994455#1994455) is a question about this.

## References [&#10548;](#tables)
* [programcreek-abstract-factory](http://www.programcreek.com/2013/02/java-design-pattern-abstract-factory/)

* [javarevisited-difference-between-factory-and-abstract-factory](http://javarevisited.blogspot.com/2013/01/difference-between-factory-and-abstract-factory-design-pattern-java.html)