---
title: Java Basic - Files and I/O
updated: 2016-06-13
layout: single
categories:
  - java-basic
tags:
  - java-basic
---

The java.io package contains nearly every class you might ever need to perform input and output (I/O) in Java.

All these streams represent an input source and an output destination.

The stream in the java.io package supports many data such as primitives, Object, localized characters, etc.

### Tables

* [Review java.io package classes](#review-javaio-package-classes-10548tables)
  * [Non-stream classes](#non-stream-classes-10548tables)
  * [Stream classes](#stream-classes-10548tables)
* [File and Directory](#file-and-directory-10548tables)
  * [Class java.io.File](#class-javaiofile-10548tables)
  * [Create file/directory](#create-filedirectory-10548tables)
  * [Listing Directories](#listing-directories-10548tables)
  * [Verifying Properties of a File/Directory](#verifying-properties-of-a-filedirectory-10548tables)
* [Layered (or Chained) I/O Streams](#layered-or-chained-io-streams-10548tables)
* [Read a file line by line](#read-a-file-line-by-line-10548tables)
* [Write a file line by line](#write-a-file-line-by-line-10548tables)
* [Append/Replace to an existing file](#appendreplace-to-an-existing-file-10548tables)
* [Standard Stream](#standard-streams-10548tables)
* [References](#references-10548tables)

The java.io package contains a relatively large number of classes, but, as you can see from these pictures following, the classes form a fairly structured hierarchy. Most of the package consists of byte streams--subclasses of *InputStream* or *OutputStream* and (in Java 1.1) character streams--subclasses of *Reader* or *Writer*. Each of these stream types has a specific purpose, and, despite its size, java.io is a straightforward package to understand and to use.

![stream_vs_character](http://www.ntu.edu.sg/home/ehchua/programming/java/images/IO_StreamVsCharacter.png)

#### The java.io package [&#10548;](#tables)

![java-io-hierarchy](http://docstore.mik.ua/orelly/java-ent/jnut/figs/JN3_1101.gif)

#### The exception classes of the java.io package

![java-io-exception-classes](http://docstore.mik.ua/orelly/java-ent/jnut/figs/JN3_1102.gif)

## Review java.io package classes [&#10548;](#tables)

### Non-stream classes [&#10548;](#tables)

* [File](#the-javaio-package-10548tables) represents a file or directory name in a system-independent way and provides methods for listing directories, querying file attributes, and renaming and deleting files.
* [FilenameFilter](#the-javaio-package-10548tables) is an interface that defines a method that accepts or rejects specified filenames. It is used by java.awt.FileDialog and File to specify what types of files should be included in directory listings.
* [RandomAccessFile](#the-javaio-package-10548tables) allows you to read from or write to arbitrary locations of a file.

Often, though, you'll prefer sequential access to a file and should use one of the:

### Stream classes [&#10548;](#tables)

* [InputStream](#the-javaio-package-10548tables) and [OutputStream](#the-javaio-package-10548tables) are abstract classes that define methods for reading and writing **bytes**. Their subclasses allow bytes to be read from and written to a variety of sources and sinks.
  * [FileInputStream](#the-javaio-package-10548tables) and [FileOutputStream](#the-javaio-package-10548tables) read from and write to files.
  * [ByteArrayInputStream](#the-javaio-package-10548tables) and [ByteArrayOutputStream](#the-javaio-package-10548tables) read from and write to an array of bytes in memory.
  * [PipedInputStream](#the-javaio-package-10548tables) reads bytes from a [PipedOutputStream](#the-javaio-package-10548tables), and **PipedOutputStream** writes bytes to a **PipedInputStream**.
* [FilterInputStream](#the-javaio-package-10548tables) and [FilterOutputStream](#the-javaio-package-10548tables) are special; they filter input and output **bytes**. When you create a **FilterInputStream**, you specify an **InputStream** for it to filter. When you call the *read()* method of a **FilterInputStream**, it calls the *read()* method of its **InputStream**, processes the **bytes** it reads, and returns the filtered bytes. Similarly, when you create a **FilterOutputStream**, you specify an **OutputStream** to be filtered. Calling the *write()* method of a **FilterOutputStream** causes it to process your **bytes** in some way and then pass those filtered bytes to the *write()* method of its **OutputStream**. **FilterInputStream** and **FilterOutputStream** do not perform any filtering themselves; this is done by their subclasses.
  * [BufferedInputStream](#the-javaio-package-10548tables) and [BufferedOutputStream](#the-javaio-package-10548tables) provide input and output buffering and can increase I/O efficiency.
  * [DataInputStream](#the-javaio-package-10548tables) reads raw bytes from a stream and interprets them in various binary formats. It has various methods to read primitive Java data types in their standard binary formats.
  * [DataOutputStream](#the-javaio-package-10548tables) allows you to write Java primitive data types in binary format.
* [Reader](#the-javaio-package-10548tables) is the superclass of all **character input streams**, and [Writer](#the-javaio-package-10548tables) is the superclass of all **character output streams**. These character streams supersede the byte streams for all textual I/O. They are more efficient than the byte streams, and they correctly handle the conversion between local encodings and Unicode text, making them invaluable for internationalized programs. Most of the Reader and Writer streams have obvious byte-stream analogs.
  * [BufferedReader](#the-javaio-package-10548tables)  is a commonly used stream; it provides buffering for efficiency and also has a *readLine()* method to read a line of text at a time.
  * [PrintWriter](#the-javaio-package-10548tables) is another very common stream; its methods allow output of a textual representation of any primitive Java type or of any object (via the object's toString() method).
* The [ObjectInputStream](#the-javaio-package-10548tables) and [ObjectOutputStream](#the-javaio-package-10548tables) classes are special. These classes are byte-stream and are part of the Object Serialization API.

## File and Directory [&#10548;](#tables)

### Class java.io.File [&#10548;](#tables)

The class java.io.File can represent either a *file* or a *directory*. [JDK 1.7 introduces a more versatile java.nio.file.Path, which overcomes many limitations of java.io.File.]

A path string is used to locate a *file* or a *directory*. Unfortunately, path strings are system dependent, e.g., "c:\myproject\java\Hello.java" in Windows or "/myproject/java/Hello.java" in Unix/Mac.

A path could be absolute (beginning from the root) or relative (which is relative to a reference directory). Special notations "." and ".." denote the current directory and the parent directory, respectively.

### Create file/directory [&#10548;](#tables)

* specificity the file/directory path
* then invoke mkdir()/mkdirs() or createNewFile() methods.
  * The **mkdir()** method creates a directory, returning true on success and false on failure. Failure indicates that the path specified in the File object already exists, or that the directory cannot be created because the entire path does not exist yet.
  * The **mkdirs()** method creates both a directory and all the parents of the directory.

#### with mkdir()
```java
import java.io.File;
public class Maker {
    public static void main(String[] args){
        try{
            File dir = new File("dir3");
            dir.mkdir();
            File file = new File(dir,"file3");
            file.createNewFile();
        }catch(Exception x){
        }
    }
}
```

#### with mkdirs()

Following example creates "/tmp/user/java/bin" directory:

```java
import java.io.File;

public class CreateDir {
   public static void main(String args[]) {
      String dirname = "/tmp/user/java/bin";
      File d = new File(dirname);
      // Create directory now.
      d.mkdirs();
  }
}
```

**Note:** Java automatically takes care of path separators on UNIX and Windows as per conventions. If you use a forward slash (/) on a Windows version of Java, the path will still resolve correctly.

### Listing Directories [&#10548;](#tables)

You can use **list()** method provided by File object to list down all the files and directories available in a directory as follows:

```java
import java.io.File;

public class ReadDir {
   public static void main(String[] args) {
      
      File file = null;
      String[] paths;
            
      try{      
         // create new file object
         file = new File("/tmp");
                                 
         // array of files and directory
         paths = file.list();
            
         // for each name in the path array
         for(String path:paths)
         {
            // prints filename and directory name
            System.out.println(path);
         }
      }catch(Exception e){
         // if any error occurs
         e.printStackTrace();
      }
   }
}
```

This would produce following result based on the directories and files available in your **/tmp** directory:

```bash
test1.txt
test2.txt
ReadDir.java
ReadDir.class
```

### Verifying Properties of a File/Directory [&#10548;](#tables)

```java
public boolean exists()       // Tests if this file/directory exists.
public long length()          // Returns the length of this file.
public boolean isDirectory()  // Tests if this instance is a directory.
public boolean isFile()       // Tests if this instance is a file.
public boolean canRead()      // Tests if this file is readable.
public boolean canWrite()     // Tests if this file is writable.
public boolean delete()       // Deletes this file/directory.
public void deleteOnExit()    // Deletes this file/directory when the program terminates.
public boolean renameTo(File dest) // Renames this file.
public boolean mkdir()        // Makes (Creates) this directory.
```

## Layered (or Chained) I/O Streams [&#10548;](#tables)

The I/O streams are often layered or chained with other I/O streams, for purposes such as buffering, filtering, or data-format conversion (between raw bytes and primitive types). For example, we can layer a BufferedInputStream to a FileInputStream for buffered input, and stack a DataInputStream in front for formatted data input (using primitives such as int, double), as illustrated in the following diagrams.

![io_layered](http://www.ntu.edu.sg/home/ehchua/programming/java/images/IO_LayeredInput.png)

## Read a file line by line [&#10548;](#tables)

The number of total classes of Java I/O is large, and it is easy to get confused when to use which. The following are two methods for reading a file line by line.

Method 1:

```java
private static void readFile1(File fin) throws IOException {
	FileInputStream fis = new FileInputStream(fin);
 
	//Construct BufferedReader from InputStreamReader
	BufferedReader br = new BufferedReader(new InputStreamReader(fis));
 
	String line = null;
	while ((line = br.readLine()) != null) {
		System.out.println(line);
	}
 
	br.close();
}
```

Method 2:

```java
private static void readFile2(File fin) throws IOException {
	// Construct BufferedReader from FileReader
	BufferedReader br = new BufferedReader(new FileReader(fin));
 
	String line = null;
	while ((line = br.readLine()) != null) {
		System.out.println(line);
	}
 
	br.close();
}
```

Use the following code:

```java
//use . to get current directory
File dir = new File(".");
File fin = new File(dir.getCanonicalPath() + File.separator + "in.txt");
 
readFile1(fin);
readFile2(fin);
```

Both works for reading a text file line by line.

The difference between the two methods is what to use to construct a BufferedReader. Method 1 uses **InputStreamReader** and Method 2 uses **FileReader**. What's the difference between the two classes?

* From Java Doc, "An InputStreamReader is a bridge from byte streams to character streams: It reads bytes and decodes them into characters using a specified charset." InputStreamReader can handle other input streams than files, such as network connections, classpath resources, ZIP files, etc.
* FileReader is "Convenience class for reading character files. The constructors of this class assume that the default character encoding and the default byte-buffer size are appropriate." FileReader does not allow you to specify an encoding other than the platform default encoding. Therefore, it is not a good idea to use it if the program will run on systems with different platform encoding.

In summary, InputStreamReader is always a safer choice than FileReader.

It is worth to mention here that instead of using a concrete / or \\ for a path, you should always use **File.separator** which can ensure that the separator is always correct for different operating systems. Also the path used should be relative, and that ensures the path is always correct.

## Write a file line by line [&#10548;](#tables)

### FileOutputStream

```java
public static void writeFile1() throws IOException {
	File fout = new File("out.txt");
	FileOutputStream fos = new FileOutputStream(fout);
 
	BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(fos));
 
	for (int i = 0; i < 10; i++) {
		bw.write("something");
		bw.newLine();
	}
 
	bw.close();
}
```

This example use FileOutputStream, instead you can use FileWriter or PrintWriter which is normally good enough for a text file operations.

### FileWriter

```java
public static void writeFile2() throws IOException {
	FileWriter fw = new FileWriter("out.txt");
 
	for (int i = 0; i < 10; i++) {
		fw.write("something");
	}
 
	fw.close();
}
```

### PrintWriter

```java
public static void writeFile3() throws IOException {
	PrintWriter pw = new PrintWriter(new FileWriter("out.txt"));
 
	for (int i = 0; i < 10; i++) {
		pw.write("something");
	}
 
	pw.close();
}
```

### OutputStreamWriter

```java
public static void writeFile4() throws IOException {
	File fout = new File("out.txt");
	FileOutputStream fos = new FileOutputStream(fout);
 
	OutputStreamWriter osw = new OutputStreamWriter(fos);
 
	for (int i = 0; i < 10; i++) {
		osw.write("something");
	}
 
	osw.close();
}
```

The main difference is that PrintWriter offers some additional methods for formatting such as println and printf. In addition, FileWriter throws IOException in case of any I/O failure. PrintWriter methods do not throws IOException, instead they set a boolean flag which can be obtained using checkError(). PrintWriter automatically invokes flush after every byte of data is written. In case of FileWriter, caller has to take care of invoking flush.

## Append/Replace to an existing file [&#10548;](#tables)

### Replace

If you want your code to create a new file and erase previous existing file, **FileWriter** can simply take it place. To **replace** all content in an existing file, use this:

```java
FileWriter fstream = new FileWriter(loc);
```

The code above will delete the existing file if it's name is use in new file being writting.

### Append/Add

To **append/add** something to an existing file, simply specify the second parameter to be true as following:

```java
FileWriter fstream = new FileWriter(loc, true);
```

This will keep adding content to the existing file instead of creating a new version.

#### Complete Example

Here is a complete code example to do this. It is nothing particularly important but a quick code reference.

```java
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
 
public class Main {
	public static void main(String[] args) throws IOException {
		File dir = new File(".");
		String loc = dir.getCanonicalPath() + File.separator + "Code.txt";
 
		FileWriter fstream = new FileWriter(loc, true);
		BufferedWriter out = new BufferedWriter(fstream);
 
		out.write("something");
		out.newLine();
 
		//close buffer writer
		out.close();
	}
}
```

## Standard Streams [&#10548;](#tables)

All the programming languages provide support for standard I/O where user's program can take input from a keyboard and then produce output on the computer screen. If you are aware if C or C++ programming languages, then you must be aware of three standard devices STDIN, STDOUT and STDERR. Similar way Java provides following three standard streams

* Standard Input: This is used to feed the data to user's program and usually a keyboard is used as standard input stream and represented as **System.in**.
* Standard Output: This is used to output the data produced by the user's program and usually a computer screen is used to standard output stream and represented as **System.out**.
* Standard Error: This is used to output the error data produced by the user's program and usually a computer screen is used to standard error stream and represented as **System.err**.

Following is a simple program which creates InputStreamReader to read standard input stream until the user types a "q":

```java
import java.io.*;

public class ReadConsole {
   public static void main(String args[]) throws IOException
   {
      InputStreamReader cin = null;

      try {
         cin = new InputStreamReader(System.in);
         System.out.println("Enter characters, 'q' to quit.");
         char c;
         do {
            c = (char) cin.read();
            System.out.print(c);
         } while(c != 'q');
      }finally {
         if (cin != null) {
            cin.close();
         }
      }
   }
}
```

```bash
$javac ReadConsole.java
$java ReadConsole
Enter characters, 'q' to quit.
1
1
e
e
q
q
```

## References [&#10548;](#tables)
* [programcreek-java-io](http://www.programcreek.com/java-io/)
* [ntu-java-io](http://www.ntu.edu.sg/home/ehchua/programming/java/j5b_io.html)