1.	Volatile in java?
    1)	the volatile keyword in Java is used as an indicator to Java compiler and Thread that do not cache value of this variable and always read it from main memory.
    2)	So what happens? Each thread has its own stack, and so its own copy of variables it can access. When the thread is created, it copies the value of all accessible variables in its own memory.
    The volatile keyword is used to say to the jvm "Warning, this variable may be modified in an other Thread". Without this keyword the JVM is free to make some optimizations,
    like never refreshing those local copies in some threads. The volatile force the thread to update the original variable for each variable. The volatile keyword could be used on every kind of variable, either primitive or objects! Maybe the subject of another article, more detailed...

2.	What is a process?
    1)	A process has a self-contained execution environment. A process generally has its own memory space.

3.	What is a Thread?
    1)	Threads are sometimes called lightweight processes. Both processes and threads provide an execution environment, but creating a new thread requires fewer resources than creating a new process.

4.	Synchronized methods vs Synchronized statements
    1)	Synchronization is a process of restricting only one thread to access the shared resource.
    2)	Static synchronized methods synchronize on the class object. If one thread is executing a static synchronized method, all other threads trying to execute any static synchronized methods will be blocked.
    3)	Non-static synchronized methods synchronize on this ie the instance of the class. If one thread is executing a synchronized method, all other threads trying to execute any synchronized methods will be blocked.
    4)	When you synchronize a method, you are effectively synchronizing to the object itself. In the case of a static method, you're synchronizing to the class of the object.
    5)	If you want to control synchronization to a specific object, or you only want part of a method to be synchronized to the object, then specify a synchronized block.

5.	Difference between wait and sleep in java?
    1)	The key point to mention while answering this question is to mention that
    wait will release the lock and must be called from the synchronized context,
    while sleep will only pause the thread for some time and keep the lock.

6.	Is it possible to start a thread twice?
    1)	No, after having started a thread by invoking its start() method, a second invocation of start() will throw an IllegalThreadStateException.

7.	Is it possible to convert a normal user thread into a daemon thread after it has been started?
    1)	A user thread cannot be converted into a daemon thread once it has been started. Invoking the method thread.setDaemon(true) on an already running thread instance causes a IllegalThreadStateException.

8.	What is Race Condition?
    1)	Race condition occurs in a multi-threaded environment when more than one thread try to access a shared resource (modify, write) at the same time. Note that it is safe if multiple threads are trying to read a shared resource as long as they are not trying to change it. Since multiple threads try to race each other to finish executing a method thus the name race condition.
    2)	Create an program to simulate Race Condition, Use TicketBooking as example
    3)	How to avoid it, using synchronized block();

9.	What is Dead lock?
    1)	Deadlock describes a situation where two or more threads are blocked forever, waiting for each other.
    2)	Deadlock can occur in a situation when a thread is waiting for an object lock, that is acquired by another thread and second thread is waiting for an object lock that is acquired by first thread. Since, both threads are waiting for each other to release the lock, the condition is called deadlock.
    3)	To avoid dead lock, avoid nested synchronized block or locks, and lock only required object, and lock the object is same order.

10.	What is Thread Dump?
    1)  A thread dump is a snapshot of the state of all threads that are part of the process. The state of each thread is presented with a so called stack trace, which shows the contents of a thread's stack. Some of the threads belong to the Java application you are running, while others are JVM internal threads.

11.	When to use ThreadDump?
    1)	When there is an obstacle, or when a Java based Web application is running much slower than expected, we need to use thread dumps.

12.	How do you check if a Thread holds a lock or not?
    1)	There is a method called holdsLock(object obj) on java.lang.Thread, it returns true if and only if the current thread holds the monitor lock on the specified object.

13.	Diffrence between Synchronized Collections vs Concurrent Collections
    1)	Synchronize means : the resource(which is synchronized) can't be modified by multiple threads simultaneously. e.g MAP returned by Collections.synchronizedMap(Map) will be a synchronized map and can be modified by one thread at a time,
    2)	Concurrent collections are exactly opposite it uses lock striping . They are called so because they allow multiple threads to concurrently access the same data. For example concurrent HashMap allows multiple threads to perform write operations in parallel as long as the writes are happening on different segments.
    3)	lock striping. Having separate locks for a portion of a data structure where each lock is locking on a variable sized set of independent objects.
    4)	A ConcurrentHashMap has a variable number of locks (default is 16) that each guard a segment of the keys in the ConcurrentHashMap. So for a ConcurrentHashMap with 160 keys, each lock will guard 10 elements. Therefore, methods operating on a key (get, put, set, etc...) only lock out access to other methods operating on a key where the keys are in the same segment. For example, if thread X calls put(0, someObject), and then thread Y calls put(10, someOtherObject) those calls can execute concurrently, and thread Y does not have to wait for thread X to return from put(0, someObject).
    5)	Additionally, certain methods such as size() and isEmpty() are not guarded at all. While this allows for greater concurrency, it means they are not strongly-consistent (they won't reflect state that is concurrently changing).

14.	Try-with-resources
    1)	The try-with-resources statement is a try statement that declares one or more resources.
    2)	The try-with-resources statement ensures that each resource is closed at the end of the statement. Any object that implements java.lang.AutoCloseable, which includes all objects which implement java.io.Closeable, can be used as a resource.