# Java Questions

## Java Threads
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
