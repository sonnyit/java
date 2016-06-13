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

[Stream](#stream)

  * [Byte Streams](#byte-streams-10548tables)
  * [Character Streams](#character-streams-10548tables)

[Standard Stream](#standard-streams-10548tables)

[Reading and Writing Files](#reading-and-writing-files-10548tables)

  * [FileInputStream](#fileinputstream-10548tables)
  * [FileOutputStream](#fileoutputstream-10548tables) 

[Directories in Java](#directories-in-java-10548tables)

  * [Creating Directories](#creating-directories-10548tables)
  * [Listing Directories](#listing-directories-10548tables)

## Stream [&#10548;](#tables)

A stream can be defined as a sequence of data. there are two kinds of Streams

* InPutStream: The InputStream is used to read data from a source.
* OutPutStream: the OutputStream is used for writing data to a destination.

## Byte Streams [&#10548;](#tables)

Java byte streams are used to perform input and output of 8-bit bytes.

Though there are many classes related to byte streams but the most frequently used classes are: **FileInputStream** and **FileOutputStream**.

Following is an example which makes use of these two classes to copy an input file into an output file:

```java
import java.io.*;

public class CopyFile {
   public static void main(String args[]) throws IOException
   {
      FileInputStream in = null;
      FileOutputStream out = null;

      try {
         in = new FileInputStream("input.txt");
         out = new FileOutputStream("output.txt");
         
         int c;
         while ((c = in.read()) != -1) {
            out.write(c);
         }
      }finally {
         if (in != null) {
            in.close();
         }
         if (out != null) {
            out.close();
         }
      }
   }
}
```

## Character Streams [&#10548;](#tables)

Java **Byte** streams are used to perform input and output of 8-bit bytes, where as Java **Character** streams are used to perform input and output for 16-bit unicode.

Though there are many classes related to character streams but the most frequently used classes are: **FileReader** and **FileWriter**.

Though internally:

* FileReader uses FileInputStream
* FileWriter uses FileOutputStream

But here major difference is that: FileReader reads two bytes at a time and FileWriter writes two bytes at a time.

We can re-write above:

```java
import java.io.*;

public class CopyFile {
   public static void main(String args[]) throws IOException
   {
      FileReader in = null;
      FileWriter out = null;

      try {
         in = new FileReader("input.txt");
         out = new FileWriter("output.txt");
         
         int c;
         while ((c = in.read()) != -1) {
            out.write(c);
         }
      }finally {
         if (in != null) {
            in.close();
         }
         if (out != null) {
            out.close();
         }
      }
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

## Reading and Writing Files [&#10548;](#tables)

As described earlier, A stream can be defined as a sequence of data. The **InputStream** is used to read data from a source and the **OutputStream** is used for writing data to a destination.

Here is a hierarchy of classes to deal with Input and Output streams.

![hierarchy of classes streams](http://www.tutorialspoint.com/java/images/file_io.jpg)

The two important streams are **FileInputStream** and **FileOutputStream**.

### FileInputStream [&#10548;](#tables)

This stream is used for reading data from the files. Objects can be created using the keyword new and there are several types of constructors available.

* Following constructor takes a file name as a string to create an input stream object to read the file:
  
  ```java
  InputStream f = new FileInputStream("C:/java/hello");
  ```
  
* Following constructor takes a file object to create an input stream object to read the file. First we create a file object using File() method:
  
  ```java
  File f = new File("C:/java/hello");
  InputStream f = new FileInputStream(f);
  ```
  
### FileOutputStream [&#10548;](#tables)

FileOutputStream is used to create a file and write data into it. The stream would create a file, if it doesn't already exist, before opening it for output.

* Constructor takes a file name as a string to create an input stream object to write the file:

  ```java
  OutputStream f = new FileOutputStream("C:/java/hello");
  ```

* Constructor takes a file object to create an output stream object to write the file. First, we create a file object using File() method:

  ```java
  File f = new File("C:/java/hello");
  OutputStream f = new FileOutputStream(f);
  ```

## Directories in Java [&#10548;](#tables)

A directory is a **File** which can contains a list of other files and directories. You use File object to create directories, to list down files available in a directory.

### Creating Directories [&#10548;](#tables)

There are two useful **File** utility methods, which can be used to create directories:

1. The **mkdir()** method creates a directory, returning true on success and false on failure. Failure indicates that the path specified in the File object already exists, or that the directory cannot be created because the entire path does not exist yet.
2. The **mkdirs()** method creates both a directory and all the parents of the directory.

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