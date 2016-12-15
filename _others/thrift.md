---
title: Thrift
updated: 2016-12-15
categories:
  - others
tags:
  - others
---

### Tables
* [Thrift Java Servers Compare](#thrift-java-servers-compare-10548tables)
  * [TSimpleServer](#tsimpleserver-10548tables)
  * [TNonblockingServer vs. THsHaServer](#tnonblockingserver-vs.-thshaserver_)
* [References](#references-10548tables)

## Thrift Java Servers Compare

List of thrift servers available for Java:

  - TSimpleServer
  - TNonblockingServer
  - THsHaServer (Half-Sync/Half-Async server)
  - TThreadedSelectorServer
  - TThreadPoolServer

### TSimpleServer

**TSimpleServer** accepts a connection, processes request from the connection until the client closes the connection, and goes back to accept a new connection. Since it is all done in a single thread with blocking I/O, it can only serve one client connection, and all the other clients will have to wait until they get accepted. TSimpleServer is mainly used for testing purpose. Don't use it in production.

### TNonblockingServer vs. THsHaServer

**TNonblockingServer** solves the problem with TSimpleServer of one client blocking all the other clients by using non-blocking I/O. It uses java.nio.channels.Selector, which allows you to get blocked on multiple connections instead of a single connection by calling select(). The select() call returns when one ore more connections are ready to be accepted/read/written. TNonblockingServer handles those connections either by accepting it, reading data from it, or writing data to it, and calls select() again to wait for the next available connections. This way, multiple clients can be served without one client starving others.

There is a catch, however. **Messages are processed by the same thread that calls select()**. Let's say there are 10 clients, and each message takes 100 ms to process. What would be the latency and throughput? While a message is being processed, 9 clients are waiting to be selected, so it takes 1 second for the clients to get the response back from the server, and throughput will be 10 requests / second. Wouldn't it be great if multiple messages can be processed simultaneously?

This is where **THsHaServer** comes into picture. It uses a single thread for network I/O, and a separate pool of worker threads to handle message processing. This way messages will get processed immediately if there is an idle worker threads, and multiple messages can be processed concurrently. Using the example above, now the latency is 100 ms and throughput will be 100 requests / sec.

## References
* [Thrift-Java-Servers-Compared](https://github.com/m1ch1/mapkeeper/wiki/Thrift-Java-Servers-Compared)
