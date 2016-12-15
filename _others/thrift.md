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
  * [TNonblockingServer vs. THsHaServer](#tnonblockingserver-vs-thshaserver-10548tables)
  * [THsHaServer vs. TThreadedSelectorServer](#thshaserver-vs-tthreadedselectorserver-10548tables)
  * [TThreadedSelectorServer vs. TThreadPoolServer](#tthreadedselectorserver-vs-tthreadpoolserver-10548tables)
  * [Conclusion](#conclusion-10548tables)
* [Compatibility in Thrift](#compatibility-in-thrift-10548tables)
  * [Example encode in Thrift](#example-encode-in-thrift-10548tables)
  * [Backward Compatible Changes -- Good!](#backward-compatible-changes----good-10548tables)
  * [Backward Incompatible Changes -- Bad!](#backward-incompatible-changes----bad-10548tables)
* [References](#references-10548tables)

## Thrift Java Servers Compare [&#10548;](#tables)

List of thrift servers available for Java:

  * [TSimpleServer](https://people.apache.org/~thejas/thrift-0.9/javadoc/org/apache/thrift/server/TSimpleServer.html)
  * [TNonblockingServer](https://people.apache.org/~thejas/thrift-0.9/javadoc/org/apache/thrift/server/TNonblockingServer.html)
  * [THsHaServer (Half-Sync/Half-Async server)](https://people.apache.org/~thejas/thrift-0.9/javadoc/org/apache/thrift/server/THsHaServer.html)
  * [TThreadedSelectorServer](https://people.apache.org/~thejas/thrift-0.9/javadoc/org/apache/thrift/server/TThreadedSelectorServer.html)
  * [TThreadPoolServer](https://people.apache.org/~thejas/thrift-0.9/javadoc/org/apache/thrift/server/TThreadPoolServer.html)

### TSimpleServer [&#10548;](#tables)

  * **TSimpleServer** accepts a connection, processes request from the connection until the client closes the connection, and goes back to accept a new connection. Since it is all done in a single thread with blocking I/O, it can only serve one client connection, and all the other clients will have to wait until they get accepted. TSimpleServer is mainly used for testing purpose. Don't use it in production.

### TNonblockingServer vs. THsHaServer [&#10548;](#tables)

* **TNonblockingServer** solves the problem with TSimpleServer of one client blocking all the other clients by using non-blocking I/O. It uses java.nio.channels.Selector, which allows you to get blocked on multiple connections instead of a single connection by calling select(). The select() call returns when one ore more connections are ready to be accepted/read/written. TNonblockingServer handles those connections either by accepting it, reading data from it, or writing data to it, and calls select() again to wait for the next available connections. This way, multiple clients can be served without one client starving others.

* There is a catch, however. **Messages are processed by the same thread that calls select()**. Let's say there are 10 clients, and each message takes 100 ms to process. What would be the latency and throughput? While a message is being processed, 9 clients are waiting to be selected, so it takes 1 second for the clients to get the response back from the server, and throughput will be 10 requests / second. Wouldn't it be great if multiple messages can be processed simultaneously?

* This is where **THsHaServer** comes into picture. It uses a single thread for network I/O, and a separate pool of worker threads to handle message processing. This way messages will get processed immediately if there is an idle worker threads, and multiple messages can be processed concurrently. Using the example above, now the latency is 100 ms and throughput will be 100 requests / sec.

### THsHaServer vs. TThreadedSelectorServer [&#10548;](#tables)

* Thrift 0.8 introduced yet another server, **TThreadedSelectorServer**. The main difference between TThreadedSelectorServer and THsHaServer is that **TThreadedSelectorServer allows you to have multiple threads for network I/O**. It maintains 2 thread pools, one for handling network I/O, and one for handling request processing. TThreadedSelectorServer performs better than THsHaServer when the network io is the bottleneck.

### TThreadedSelectorServer vs. TThreadPoolServer [&#10548;](#tables)

* Finally, there is **TThreadPoolServer**. TThreadPoolServer is different from the other 3 servers in that:

  * There is a dedicated thread for accepting connections.
  * Once a connection is accepted, it gets scheduled to be processed by a worker thread in ThreadPoolExecutor.
  * **The worker thread is tied to the specific client connection until it's closed**. Once the connection is closed, the worker thread goes back to the thread pool.
  * You can configure both minimum and maximum number of threads in the thread pool. Default values are 5 and Integer.MAX_VALUE, respectively.

  This means that if there are 10000 concurrent client connections, you need to run 10000 threads. As such, it is not as resource friendly as other servers. Also, if the number of clients exceeds the maximum number of threads in the thread pool, requests will be blocked until a worker thread becomes available.

### Conclusion [&#10548;](#tables)

> The general conclusion of the research is that TThreadedSelectorServer would be the best solution in most cases. TThreadPoolServer offers better throughput but at the expense of running many concurrent threads.
(from [Learning Apache Thrift - page155](https://www.packtpub.com/application-development/learning-apache-thrift))

>  I think TThreadedSelectorServer would be a safe choice for most of the use cases. You might also want to consider TThreadPoolServer if you can afford to run lots of concurrent threads. (from the author of original article)

In my opinion:

  * If workers have to handle heavy task, and you do not have too too much concurrent client (mean network io is not bottleneck) -> so *THsHaServer* is a good choice.
  * In case we have a lots of concurrent client, and if the task for each worker is heavy -> *TThreadPoolServer*, else, choose *TThreadedSelectorServer*.

## Compatibility in Thrift [&#10548;](#tables)

### Example encode in Thrift [&#10548;](#tables)

The example will using a little object describing a person. In JSON:

```json
{
      "userName": "Martin",
      "favouriteNumber": 1337,
      "interests": ["daydreaming", "hacking"]
}
```

This JSON encoding can be our baseline. If remove all the whitespace it consumes 82 bytes.

In Thrift IDL, all the encodings share the same schema definition:

```
struct Person {
    1: string       userName,
    2: optional i64 favouriteNumber,
    3: list<string> interests
}
```

Some of the protocols available for majority of the Thrift-supported languages are:

* binary: Fairly simple binary encoding -- the length and type of a field are encoded as bytes followed by the actual value of the field.
* compact: Described in THRIFT-110
* json

The BinaryProtocol encoding is very straightforward, but also fairly wasteful (it takes 59 bytes to encode our example record):

![Thrift BinaryProtocol](https://martin.kleppmann.com/2012/12/binaryprotocol.png)

The CompactProtocol encoding is semantically equivalent, but uses variable-length integers and bit packing to reduce the size to 34 bytes:

![Thrift CompactProtocol](https://martin.kleppmann.com/2012/12/compactprotocol.png)

As you can see, each field is manually assigned a tag in the IDL, and the tags and field types are stored in the binary encoding, which enables the parser to skip unknown fields.

[for more detail, please read original article](https://martin.kleppmann.com/2012/12/05/schema-evolution-in-avro-protocol-buffers-thrift.html)

### Backward Compatible Changes -- Good! [&#10548;](#tables)

* Adding new methods or structs
* Adding a non-required field to a struct
* Changing a method return type from void to anything else
* Removing an exception from a method signature
* Removing a field from a struct
* Renaming a field in a struct
* Renaming a struct
* Adding an argument to a method with or without a default value
* Removing an argument from a method
* Changing the order of arguments in a method
* Changing the namespace

These changes will still allow older clients to connect to the new version of the server.

### Backward Incompatible Changes -- Bad! [&#10548;](#tables)

The following changes require all clients to update their stubs to the latest versions generated. Clients connecting with older versions of the stubs will get exceptions on their method invocations.

* Removing or renaming a method
* Changing the type of an argument in a method
* Changing the declared type of a return value, or changing it to void
* Adding an exception to a method (with a non-void return type)

Adding an exception to any method should really be considered to break backward compatibility, but an oddity of thrift's implementation is that if you throw an exception from the server that is not expected by the client, it will just be ignored, but only if the method is declared void.

## References [&#10548;](#tables)
* [Thrift-Java-Servers-Compared](https://github.com/m1ch1/mapkeeper/wiki/Thrift-Java-Servers-Compared)
* [thrift-versioning-doc](https://github.com/bkayser/thrift-versioning-doc)
* [schema-evolution-in-avro-protocol-buffers-thrift](https://martin.kleppmann.com/2012/12/05/schema-evolution-in-avro-protocol-buffers-thrift.html)
