---
title: Java Multithreading
updated: 2016-07-19
categories:
  - java-advance
tags:
  - java-advance
---

### Tables

* [Introduction](#introduction-10548tables)
	* [Thread vs Process in Java](#thread-vs-process-in-java-10548tables)
	* [Multitasking vs Multithreading vs Multiprocessing vs parallel processing](#multitasking-vs-multithreading-vs-multiprocessing-vs-parallel-processing-10548tables)
* [Life cycle of a Thread](#life-cycle-of-a-thread-10548tables)
* [Thread priorities](#thread-priorities-10548tables)
* [Create a thread in Java](#create-a-thread-in-java-10548tables)
	* [Thread creation by extending Thread class](#thread-creation-by-extending-thread-class-10548tables)
	* [Thread creation by implementing Runable Interface](#thread-creation-by-implementing-runable-interface-10548tables)
* [Method: isAlive() and join()](#method-isalive-and-join-10548tables)
* [Synchronization](#synchronization-10548tables)
* [Inter-thread Communication](#inter-thread-communication-10548tables)
* [References](#references-10548tables)
 

## Introduction [&#10548;](#tables)

### Thread vs Process in Java [&#10548;](#tables)

1. Both process and Thread are independent path of execution but one process can have multiple Threads.
2. Every process has its own memory space, executable code and a unique process identifier (PID) while every thread has its own stack in Java but it uses process main memory and share it with other threads.
3. Threads are also refereed as task or light weight process (LWP) in operating system.
4. Threads from same process can communicate with each other by using Programming language construct like [wait and notify in Java](http://javarevisited.blogspot.sg/2011/05/wait-notify-and-notifyall-in-java.html) and much simpler than inter process communication.
5. Another difference between Process and Thread in Java is: how Thread and process are created. It's easy to create Thread as compared to Process which requires duplication of parent process.
6. All Threads which is part of same process share system resource like file descriptors, Heap Memory and other resource but each Thread has its own Exception handler and own stack in Java.

### Multitasking vs Multithreading vs Multiprocessing vs parallel processing [&#10548;](#tables)

* **Multitasking:** Ability to execute more than one task at the same time is known as multitasking.
* **Multithreading:** It is a process of executing multiple threads simultaneously. Multithreading is also known as Thread-based Multitasking.
* **Multiprocessing:** It is same as multitasking, however in multiprocessing more than one CPUs are involved. On the other hand one CPU is involved in multitasking.
* **Parallel Processing:** It refers to the utilization of multiple CPUs in a single computer system.

## Life cycle of a Thread [&#10548;](#tables)

A thread goes through various stages in its life cycle. For example, a thread is born, started, runs, and then dies. Following diagram shows complete life cycle of a thread.

![thread-life-cycle](http://www.tutorialspoint.com/java/images/Thread_Life_Cycle.jpg)

A thread can be in one of the following states:

* **New:** A new thread begins its life cycle in the new state. It remains in this state until the program starts the thread. It is also referred to as a born thread.
* **Runnable:** After a newly born thread is started, the thread becomes runnable. A thread in this state is considered to be executing its task.
* **Waiting:** Sometimes, a thread transitions to the waiting state while the thread waits for another thread to perform a task.A thread transitions back to the runnable state only when another thread signals the waiting thread to continue executing.
* **Timed waiting:** A runnable thread can enter the timed waiting state for a specified interval of time. A thread in this state transitions back to the runnable state when that time interval expires or when the event it is waiting for occurs.
* **Terminated ( Dead ):** A runnable thread enters the terminated state when it completes its task or otherwise terminates.

## Thread priorities [&#10548;](#tables)

Every Java thread has a priority that helps the operating system determine the order in which threads are scheduled.

Java thread priorities are in the range between MIN_PRIORITY (a constant of 1) and MAX_PRIORITY (a constant of 10). By default, every thread is given priority NORM_PRIORITY (a constant of 5).

Threads with higher priority are more important to a program and should be allocated processor time before lower-priority threads. However, thread priorities cannot guarantee the order in which threads execute and very much platform dependent.

To set the priority of the thread setPriority() method is used which is a method of the class Thread Class.

## Create a thread in Java [&#10548;](#tables)

There are two ways to create a thread in Java:

1. By extending Thread class.
2. By implementing Runnable interface.

Before we begin with the programs(code) of creating threads, let’s have a look at these methods of Thread class. We have used few of these methods in the example below.

* getName(): It is used for Obtaining a thread’s name
* getPriority(): Obtain a thread’s priority
* isAlive(): Determine if a thread is still running
* join(): Wait for a thread to terminate
* run(): Entry point for the thread. The join() method must be place in a try catch block
* sleep(): suspend a thread for a period of time
* start(): start a thread by calling its run() method

### Thread creation by extending Thread class [&#10548;](#tables)

#### Step 1
You will need to override **run( )** method available in Thread class. This method provides entry point for the thread and you will put you complete business logic inside this method. Following is simple syntax of **run()** method:

```java
public void run( )
```

#### Step 2
Once Thread object is created, you can start it by calling **start( )** method, which executes a call to **run( )** method. Following is simple syntax of **start()** method:

```java
void start( );
```

#### Example

```java
class ThreadDemo extends Thread {
   private Thread t;
   private String threadName;
   
   ThreadDemo(String name){
       threadName = name;
       System.out.println("Creating " +  threadName );
   }
   public void run() {
      System.out.println("Running " +  threadName );
      try {
         for(int i = 4; i > 0; i--) {
            System.out.println("Thread: " + threadName + ", " + i);
            // Let the thread sleep for a while.
            Thread.sleep(50);
         }
     } catch (InterruptedException e) {
         System.out.println("Thread " +  threadName + " interrupted.");
     }
     System.out.println("Thread " +  threadName + " exiting.");
   }
   
   public void start ()
   {
      System.out.println("Starting " +  threadName );
      if (t == null)
      {
         t = new Thread (this, threadName);
         t.start ();
      }
   }
}

public class TestThread {
   public static void main(String args[]) {
   
      ThreadDemo T1 = new ThreadDemo("Thread-1");
      T1.start();
      
      ThreadDemo T2 = new ThreadDemo("Thread-2");
      T2.start();
   }   
}
```

Output:

```bash
Creating Thread-1
Starting Thread-1
Creating Thread-2
Starting Thread-2
Running Thread-1
Thread: Thread-1, 4
Running Thread-2
Thread: Thread-2, 4
Thread: Thread-1, 3
Thread: Thread-2, 3
Thread: Thread-1, 2
Thread: Thread-2, 2
Thread: Thread-1, 1
Thread: Thread-2, 1
Thread Thread-1 exiting.
Thread Thread-2 exiting.
```

### Thread creation by implementing Runable Interface [&#10548;](#tables)

#### Step 1
As a first step you need to implement a **run()** method provided by Runnable interface. This method provides entry point for the thread and you will put you complete business logic inside this method. Following is simple syntax of **run()** method:

```java
public void run( )
```

#### Step 2
At second step you will instantiate a Thread object using the following constructor:

```java
Thread(Runnable threadObj, String threadName);
```

Where, *threadObj* is an instance of a class that implements the Runnable interface and *threadName* is the name given to the new thread.

#### Step 3
Once Thread object is created, you can start it by calling **start( )** method, which executes a call to **run( )** method. Following is simple syntax of **start()** method:

```java
void start( );
```

#### Example

```java
class RunnableDemo implements Runnable {
   private Thread t;
   private String threadName;
   
   RunnableDemo( String name){
       threadName = name;
       System.out.println("Creating " +  threadName );
   }
   public void run() {
      System.out.println("Running " +  threadName );
      try {
         for(int i = 4; i > 0; i--) {
            System.out.println("Thread: " + threadName + ", " + i);
            // Let the thread sleep for a while.
            Thread.sleep(50);
         }
     } catch (InterruptedException e) {
         System.out.println("Thread " +  threadName + " interrupted.");
     }
     System.out.println("Thread " +  threadName + " exiting.");
   }
   
   public void start ()
   {
      System.out.println("Starting " +  threadName );
      if (t == null)
      {
         t = new Thread (this, threadName);
         t.start ();
      }
   }

}

public class TestThread {
   public static void main(String args[]) {
   
      RunnableDemo R1 = new RunnableDemo( "Thread-1");
      R1.start();
      
      RunnableDemo R2 = new RunnableDemo( "Thread-2");
      R2.start();
   }   
}
```

Output:

```bash
Creating Thread-1
Starting Thread-1
Creating Thread-2
Starting Thread-2
Running Thread-1
Thread: Thread-1, 4
Running Thread-2
Thread: Thread-2, 4
Thread: Thread-1, 3
Thread: Thread-2, 3
Thread: Thread-1, 2
Thread: Thread-2, 2
Thread: Thread-1, 1
Thread: Thread-2, 1
Thread Thread-1 exiting.
Thread Thread-2 exiting.
```

## Method: isAlive() and join() [&#10548;](#tables)

* Main thread should finish last else other threads which have spawned from the main thread will also finish.
* To know whether the thread has finished we can call **isAlive()** on the thread which returns true if the thread is not finished.
* Another way to achieve this by using **join()** method, this method when called from the parent thread makes parent thread wait till child thread terminates. The join() method must be place in a try catch block.
* These methods are defined in the Thread class.
* However, **wait()**, **notify()**, **notifyAll()** are defined in the Object class.

## Synchronization [&#10548;](#tables)

* Multithreading introduces asynchronous behavior to the programs. If a thread is writing some data another thread may be reading the same data at that time. This may bring inconsistency.
* When two or more threads need access to a shared resource there should be some way that the resource will be used only by one resource at a time. The process to achieve this is called synchronization.
* To implement the synchronous behavior java has synchronous method. Once a thread is inside a synchronized method, no other thread can call any other synchronized method on the same object. * All the other threads then wait until the first thread come out of the synchronized block.
* When we want to synchronize access to objects of a class which was not designed for the multithreaded access and the code of the method which needs to be accessed synchronously is not available with us, in this case we cannot add the synchronized to the appropriate methods. In java we have the solution for this, put the calls to the methods (which needs to be synchronized) defined by this class inside a synchronized block in following manner.

```java
Synchronized(object)
{
    // statement to be synchronized
}
```

## Inter-thread Communication [&#10548;](#tables)

We have few methods through which java threads can communicate with each other. These methods are **wait()**, **notify()**, **notifyAll()**. All these methods can only be called from within a synchronized method.

1. To understand synchronization java has a concept of monitor. Monitor can be thought of as a box which can hold only one thread. Once a thread enters the monitor all the other threads have to wait until that thread exits the monitor.
2. **wait()** tells the calling thread to give up the monitor and go to sleep until some other thread enters the same monitor and calls notify().
3. **notify()** wakes up the first thread that called wait() on the same object.
4. **notifyAll()** wakes up all the threads that called wait() on the same object. The highest priority thread will run first.

## References [&#10548;](#tables)
* [tutorialspoint-java-multithreading](http://www.tutorialspoint.com/java/java_multithreading.htm)
* [java67-thread-vs-process](http://www.java67.com/2012/12/what-is-difference-between-thread-vs-process-java.html)
* [beginnersbook-multithreading-in-java](http://beginnersbook.com/2013/03/multithreading-in-java/)