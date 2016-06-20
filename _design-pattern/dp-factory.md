---
title: Design Pattern - Factory
updated: 2016-06-20
layout: single
categories:
  - java-design-pattern
tags:
  - java-design-pattern
---

### Tables

* [The story for Factory pattern](#the-story-for-factory-pattern-10548tables)
* [Factory pattern class diagram](#factory-pattern-class-diagram-10548tables)
* [Factory pattern Java code](#factory-pattern-java-code-10548tables)
* [References](#references-10548tables)

## The story for Factory pattern [&#10548;](#tables)

**Factory design pattern** is used for creating an object based on different parameters.

The example below is about creating human in a factory. If we ask the factory for a boy, the factory will produce a boy; if we ask for a girl, the factory will produce a girl. Based on different parameters, the factory produce different stuff.

## Factory pattern class diagram [&#10548;](#tables)

![factory-design-pattern](http://www.programcreek.com/wp-content/uploads/2013/02/factory-design-pattern.png)

## Factory pattern Java code [&#10548;](#tables)

```java
interface Human {
	public void Talk();
	public void Walk();
}
 
 
class Boy implements Human{
	@Override
	public void Talk() {
		System.out.println("Boy is talking...");		
	}
 
	@Override
	public void Walk() {
		System.out.println("Boy is walking...");
	}
}
 
class Girl implements Human{
 
	@Override
	public void Talk() {
		System.out.println("Girl is talking...");	
	}
 
	@Override
	public void Walk() {
		System.out.println("Girl is walking...");
	}
}
 
public class HumanFactory {
	public static Human createHuman(String m){
		Human p = null;
		if(m.equals("boy")){
			p = new Boy();
		}else if(m.equals("girl")){
			p = new Girl();
		}
 
		return p;
	}
}
```

## References [&#10548;](#tables)

* [programcreek-factory-pattern](http://www.programcreek.com/2013/02/java-design-pattern-factory/)