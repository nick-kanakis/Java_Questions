# Java Questions

## Threads
> What is the difference between processes and threads.

A process is an execution of a program, while a Thread is a single execution sequence within a process. A process can contain multiple threads.

> Different ways of creating a thread.

1. Extend the ```Thread``` class.
2. Implement ```Runnable``` interface. Preferred in case you need to extend another class other than ```Thread```.
3. Use the ```Executor``` framework to create a thread pool.

> Thread states.

1. ```New```  Thread becomes ready to run, but does not necessarily start running immediately
2. ```Runnable``` JVM is now running this thread.
3. ```Blocked``` Thread is blocked waiting for acquiring a lock.
4. ```Waiting``` Thread waits another thread to complete an action.
5. ```Time Waiting```Thread waits another thread to complete an action, UNTIL a specified time.
6. ```Terminated``` Thread finished execution.


## Collection
> fail-fast vs fail-safe ?

The Iterator's fail-safe property works with the clone of the underlying collection and thus, it is not affected by any modification in the collection. All the collection classes in ```java.util package``` are fail-fast, while the collection classes in ```java.util.concurrent``` are fail-safe.

> hashCode() and equals() methods.

 Java, a HashMap uses the hashCode and equals methods to determine the index of the key-value pair and to detect duplicates. More specifically, the hashCode method is used in order to determine where the specified key will be stored. Since different keys may produce the same hash value, the equals method is used, in order to determine whether the specified key actually exists in the collection or not.
 
Eg: If a PhoneNumber object's equality is based on the number is passed as argument, this will not work:
```
Map<PhoneNumber, String> m = new HashMap<>();
m.put(new PhoneNumber(2109412422), "Jenny");
m.get(new PhoneNumber(2109412422)) // will return null'
```

> HashMap vs Hashtable.

- A Hashtable is synchronized, while a HashMap is not. Thus, HashMap is preferred in single-threaded environments, while a Hashtable is suitable for multi-threaded environments.
- The Hashtable class is considered to be a legacy class.

> ArrayList vs LinkedList.

- ArrayList provide O(1) retrieval time because are backed by an Array. Linkedlist need O(n) retrieval time as it stores its data as a list of elements and every element is linked to its previous and next element.

- The Insertion, addition and removal operations of an element are faster in a LinkedList compared to an ArrayList, because there is no need of resizing an array or updating the index when an element is added in some arbitrary position inside the collection.

> Comparable vs Comparator.

```Comparator``` provides a way for you to provide custom comparison logic for types that you have no control over.
```Comparable``` allows you to specify how objects that you are implementing get compared.

> Enumaration vs Iterator.

Both will give successive elements, but Iterator is improved in such a way so the method names are shorter, and has an additional remove method. Always prefer Iterator.

> HashSet vs TreeSet.

HashSet is implemented using a hash table and thus, its elements are not ordered. The add, remove, and contains methods of a HashSet have constant time complexity O(1). On the other hand, a TreeSet is implemented using a tree structure. The elements in a TreeSet are sorted, and thus, the add, remove, and contains methods have time complexity of O(logn).

## JVM & Garbage Collectors

> Describe the JVM high level.

The code you write is in a .java file. Java compliler (javac) compiles the code to bytecode .class class. and this is passed to the JVM.
JVM has 3 main parts:

- **Classloader**. Loads dynamically the classes in the JVM.
- **Execution engine**. Translates bytecode to machine code and run the commands.
- **Runtime data area**. Runtime memory.

> What is a classLoader.

Loads dynamically the classes in the JVM. Classloaders are hierarchical.

1. Bootstrap classloader. Parrent of all classloaders instances, loads interal JDK instances.
2. Extension classloader. Child of Bootstrap classloader, loads extension classes like Logger.
3. System classloader. Child of Extension classloader, loads applicaiton classes.
4. (OPTIONAL) custom clasloader. Child of system classloader, defined by the developer, it may be used to load classes from external systems like DB or over the network.

When a system classloader wants a clas and it does not have it, it delegates to it's parent (extension classloader) and againt if it is not available here to the bootstrap classloader. The visibility is always BOTTOM -> TOP.

> Runtime Data areas.

Is the memory area of the JVM is devided in 3 parts:
- Memory of each thread (stack). Stack is created per Thread and hold the methods/local variables of the thread as well as references to classes in the heap.
- Common memory of all threads (heap). It stores classes & instances of objects, is the target of the GC.
- Metaspace. By default auto increases its size, holds any static reference.

> Garbage collector & Finalize().

Object that are eligible for gc are objects that are unreachable from the object graph. Multiple objects can be unreachable (see isolation island).

All objects are stored in Eden space. When Eden space is full a minor gc occures and everything that survices goes to Survivor space (S0) and after some rounds of gc to (S1).

After X rounds surving objects will be moved to Old space. Here gc in not often, but when it happens it stops everything ("stop the world")

> Types of references in JVM.

- Strong. Created by "new" keyword, will be garbage collected.
- Weak. Will propable not survive the next gc. WeakReference<MyObject> newWeakReference = new WeakReference<>(new MyObject());
- Soft. Will be gc only if there is not memory available. SoftReference<MyObject> newWeakReference = new SoftReference<>(new MyObject());

> Finalizers & cleaners.

Finalize() and clean() are methods that are called just before destroying an object. It is normally advised to release resources held by the object inside the finalize method. 

SOS: It is just a suggetion to the compiler.

> Types of GC.

- Serial. For smaller cpus, one thread is used.
- Parallel. Multiple threads are used but in old space only 1 thread is still used.
- Parallel old. Multiple threads are used even in old space.
- CMS. < 1.7 target was to minimize the pause time. 
- G1 GC. Replacement of CMS.

> Execution engine.

Reads the bytecode & executes it.

- Interpreter. Reads, interpretes to machine code & executes bytecode.
- JIT. Just In Time compliler, is used in frequently used code parts, it compiles to native c/c++ the code and do not use interpreter any more for this part.

## JDBC

> What is JDBC ? 

JDBC is an abstraction layer that allows users to choose between databases. JDBC enables developers to write database applications in Java, without having to concern themselves with the underlying details of a particular database.

> What does Connection pooling mean ? 

The interaction with a database can be costly, regarding the opening and closing of database connections. Especially, when the number of database clients increases, this cost is very high and a large number of resources is consumed.A pool of database connections is obtained at start up by the application server and is maintained in a pool. A request for a connection is served by a connection residing in the pool. In the end of the connection, the request is returned to the pool and can be used to satisfy future requests.

## Servlets

> What is a Servlet ? 

 The servlet is a Java programming language class used to process client requests and generate dynamic web content. Servlets are mostly used to process or store data submitted by an HTML form, provide dynamic content and manage state information that does not exist in the stateless HTTP protocol.
 
 > Arhitechure of a Servlet.
 
 The core abstraction that must be implemented by all servlets is the ```javax.servlet.Servlet``` interface. Each servlet must implement it either directly or indirectly, either by extending ```javax.servlet.GenericServlet``` or ```javax.servlet.http.HTTPServlet```. Finally, each servlet is able to serve multiple requests in parallel using multithreading. Generic Servlet is a generic, protocol independent servlet, HttpServlet is a servlet tied specifically to the HTTP protocol.
 
 > Life cycle of a Servlet.
 
On every client’s request, the Servlet Engine loads the servlets and invokes its **init** methods, in order for the servlet to be initialized. Then, the Servlet object handles all subsequent requests coming from that client, by invoking the service method for each request separately. Finally, the servlet is removed by calling the server’s **destroy** method.

> Structure of the HTTP response.

- **Status Code**: Describes the status of the response. It can be used to check if the request has been successfully completed.
- **HTTP Headers**: Contains more information about the response. For example, the headers may specify the date/time after which the response is considered stale, or the form of encoding used to safely transfer the entity to the user.
- **Body**: Contains the content of the response. The body may contain HTML code, an image, etc. The body consists of the data bytes transmitted in an HTTP transaction message immediately following the headers

> What is a cookie ? What is the difference between session and cookie ?

A cookie is a bit of information that the Web server sends to the browser. The browser stores the cookies for each Web server in a local file. In a future request, the browser, along with the request, sends all stored cookies for that specific Web server.The differences between session and a cookie are the following:

- Session should work, regardless of the settings on the client browser. The client may have chosen to disable cookies. However, the sessions still work, as the client has no ability to disable them in the server side.
- The HTTP session is capable of storing any Java object, while a cookie can only store String objects.


