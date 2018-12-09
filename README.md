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



