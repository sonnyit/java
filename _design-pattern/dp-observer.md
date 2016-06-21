---
title: Design Pattern - Observer
updated: 2016-06-21
layout: single
categories:
  - java-design-pattern
tags:
  - java-design-pattern
---

### Tables

* [What is Observer design Pattern?](#what-is-observer-design-pattern-10548tables)
  * [Definition](#definition-10548tables)
  * [Explanation](#explanation-10548tables)
  * [Class diagram](#class-diagram-10548tables)
  * [Advantages and Disadvantages](#advantages-and-disadvantages-10548tables)
  * [When to use this pattern?](#when-to-use-this-pattern-10548tables)
* [Observer pattern Java code](#observer-pattern-java-code-10548tables)
  * [Story of problem](#story-of-problem-10548tables)
  * [Class diagram](#class-diagram-10548tables)
  * [Java code](#java-code-10548tables)
* [References](#references-10548tables)

## What is Observer design Pattern? [&#10548;](#tables)

To understand **Observer Pattern**, first need to understand the subject and observer objects.

The relation between subject and observer can easily be understood as an analogy to magazine subscription.

* A magazine publisher(subject) is in the business and publishes magazines (data).
* If you (user of data/observer) are interested in the magazine you subscribe (register), and if a new edition is published it gets delivered to you.
* If you unsubscribe(unregister) you stop getting new editions.
* Publisher doesn't know who you are and how you use the magazine, it just delivers it to you because you are a subscriber(loose coupling).

### Definition [&#10548;](#tables)

The **Observer Pattern** defines a one to many dependency between objects so that one object changes state, all of its dependents are notified and updated automatically.

### Explanation [&#10548;](#tables)

* One to many dependency is between Subject(One) and Observer(Many).
* There is dependency as Observers themselves don't have access to data. They are dependent on Subject to provide them data.

### Class diagram [&#10548;](#tables)

![class-diagram](http://d1gjlxt8vb0knt.cloudfront.net//wp-content/uploads/o2.png)

* Here Observer and Subject are interfaces(can be any abstract super type not necessarily java interface).
* All observers who need the data need to implement observer interface.
notify() method in observer interface defines the action to be taken when the subject provides it data.
* The subject maintains an observerCollection which is simply the list of currently registered(subscribed) observers.
* registerObserver(observer) and unregisterObserver(observer) are methods to add and remove observers respectively.
* notifyObservers() is called when the data is changed and the observers need to be supplied with new data.

### Advantages and Disadvantages [&#10548;](#tables)

#### Advantages

Provides a loosely coupled design between objects that interact. Loosely coupled objects are flexible with changing requirements. Here loose coupling means that the interacting objects should have less information about each other.

Observer pattern provides this loose coupling as:

Subject only knows that observer implement Observer interface.Nothing more.
There is no need to modify Subject to add or remove observers.
We can reuse subject and observer classes independently of each other.

#### Disadvantages

Memory leaks caused by Lapsed listener problem because of explicit register and unregistering of observers.


### When to use this pattern? [&#10548;](#tables)

You should consider using this pattern in your application when multiple objects are dependent on the state of one object as it provides a neat and well tested design for the same.

#### Real Life Uses:

* It is heavily used in GUI toolkits and event listener. In java the button(subject) and onClickListener(observer) are modelled with observer pattern.
* Social media, RSS feeds, email subscription in which you have the option to follow or subscribe and you receive latest notification.
* All users of an app on play store gets notified if there is an update.

## Observer pattern Java code [&#10548;](#tables)

### Story of problem [&#10548;](#tables)

Suppose we are building a cricket app that notifies viewers about the information such as current score, run rate etc. Suppose we have made two display elements CurrentScoreDisplay and AverageScoreDisplay. CricketData has all the data (runs, bowls etc.) and whenever data changes the display elements are notified with new data and they display the latest data accordingly

### Class diagram [&#10548;](#tables)

![diagram](http://d1gjlxt8vb0knt.cloudfront.net//wp-content/uploads/o3.png)

### Java code [&#10548;](#tables)

```java
// Java program to demonstrate working of
// onserver pattern
import java.util.ArrayList;
import java.util.Iterator;
 
// Implemented by Cricket data to communicate
// with observers
interface Subject
{
    public void registerObserver(Observer o);
    public void unregisterObserver(Observer o);
    public void notifyObservers();
}
 
class CricketData implements Subject
{
    int runs;
    int wickets;
    float overs;
    ArrayList<Observer> observerList;
 
    public CricketData() {
        observerList = new ArrayList<Observer>();
    }
 
    @Override
    public void registerObserver(Observer o) {
        observerList.add(o);
    }
 
    @Override
    public void unregisterObserver(Observer o) {
        observerList.remove(observerList.indexOf(o));
    }
 
    @Override
    public void notifyObservers()
    {
        for (Iterator<Observer> it =
              observerList.iterator(); it.hasNext();)
        {
            Observer o = it.next();
            o.update(runs,wickets,overs);
        }
    }
 
    // get latest runs from stadium
    private int getLatestRuns()
    {
        // return 90 for simplicity
        return 90;
    }
 
    // get latest wickets from stadium
    private int getLatestWickets()
    {
        // return 2 for simplicity
        return 2;
    }
 
    // get latest overs from stadium
    private float getLatestOvers()
    {
        // return 90 for simplicity
        return (float)10.2;
    }
 
    // This method is used update displays
    // when data changes
    public void dataChanged()
    {
        //get latest data
        runs = getLatestRuns();
        wickets = getLatestWickets();
        overs = getLatestOvers();
 
        notifyObservers();
    }
}
 
// This interface is implemented by all those
// classes that are to be updated whenever there
// is an update from CricketData
interface Observer
{
    public void update(int runs, int wickets,
                      float overs);
}
 
class AverageScoreDisplay implements Observer
{
    private float runRate;
    private int predictedScore;
 
    public void update(int runs, int wickets,
                       float overs)
    {
        this.runRate =(float)runs/overs;
        this.predictedScore = (int)(this.runRate * 50);
        display();
    }
 
    public void display()
    {
        System.out.println("\nAverage Score Display: \n"
                           + "Run Rate: " + runRate +
                           "\nPredictedScore: " +
                           predictedScore);
    }
}
 
class CurrentScoreDisplay implements Observer
{
    private int runs, wickets;
    private float overs;
 
    public void update(int runs, int wickets,
                       float overs)
    {
        this.runs = runs;
        this.wickets = wickets;
        this.overs = overs;
        display();
    }
 
    public void display()
    {
        System.out.println("\nCurrent Score Display:\n"
                           + "Runs: " + runs +
                           "\nWickets:" + wickets +
                           "\nOvers: " + overs );
    }
}
 
// Driver Class
class Main
{
    public static void main(String args[])
    {
        // create objects for testing
        AverageScoreDisplay averageScoreDisplay =
                          new AverageScoreDisplay();
        CurrentScoreDisplay currentScoreDisplay =
                          new CurrentScoreDisplay();
 
        // pass the displays to Cricket data
        CricketData cricketData = new CricketData();
 
        // register display elements
        cricketData.registerObserver(averageScoreDisplay);
        cricketData.registerObserver(currentScoreDisplay);
 
        // in real app you would have some logic to
        // call this function when data changes
        cricketData.dataChanged();
 
        //remove an observer
        cricketData.unregisterObserver(averageScoreDisplay);
 
        // now only currentScoreDisplay gets the
        // notification
        cricketData.dataChanged();
    }
}
```

Output:

```bash
Average Score Display: 
Run Rate: 8.823529
PredictedScore: 441

Current Score Display:
Runs: 90
Wickets:2
Overs: 10.2

Current Score Display:
Runs: 90
Wickets:2
Overs: 10.2
```

## References [&#10548;](#tables)
* [geeksforgeeks-observer-set1](http://www.geeksforgeeks.org/observer-pattern-set-1-introduction/)
* [geeksforgeeks-observer-set2](http://www.geeksforgeeks.org/observer-pattern-set-2-implementation/)
* [programcreek-observer](http://www.programcreek.com/2011/01/an-java-example-of-observer-pattern/)