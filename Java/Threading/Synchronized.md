# Synchronized

## Synchronous vs Asynchronous



##  Volatile

Means to not cache the variable. Caching can allow the variable to be read faster, but when a value is getting changed in a thread, you want to see the actual value rather than the cache which could be an old value and so it could lead to a dirty read.

Using `volatile` reduces the risk of memory consistency errors, because any write to a volatile variable establishes a happens-before relationship with subsequent reads of that same variable, meaning that changes to a volatile variable are always visible to other threads.

```java
public volatile int count = 0;
```

## Synchronized

A **shared object** may have synchronized methods or code blocks to be executed with mutual.

The `synchronized` keyword turns a method synchronized by defining mutual exclusion for an entire method or a code block. The synchronized block should be short and contain the <u>critical section</u>  and contain no extra information.  This is because a synchronized method will lock other threads until it finishes running.

### Steps

1. Each object has an **implicit lock** (placed by the program) associated with the object
2. Each object has also one implicit condition variable called **wait set**
3. Each synchronized block requires a lock object to be explicitly indicated
4. A thread must obtain the lock when calling a synchronized method or block 
5. A thread may wait on and signal to the wait set

### Unsynchronized Example

```java
private volatile int count = 0;

public static void main(String[] args) {
    Class class = new Class();
    class.doWork();
}

public void doWork() {
    Runnable r = () -> {
        for(int i = 0; i < 10000; i++) {
            count++;
        }
    }
    
    Thread t1 = new Thread(runnable);
    Thread t2 = new Thread(runnable);
    
    t1.start();
    t2.start();
    try {
        t1.join();
        t2.join();
    } catch(Exception e) {
        //Catch Statement
    }    
}

//OUTPUT: 13000...14000...10000...20000
//As can be seen, output is not consistent, and it is not 20000 everytime
```

### Synchronized Method Example

In order for it to be synchronized, the count variable must be incremented in a synchronized method. Just create a `synchronized` method that increases the value of count by 1. Inside the for loop of the `run()` method, use the `increment()` method instead of `count++`

```java
public synchronized void increment() {
    count++;
}
```

### Synchronized Block Example

```java
Runnable r = () -> {
    synchronized(this) {
        for(int i = 0; i < 10000; i++) {
            count++;
        }
    }
}
```

## Guarded Blocks

Threads have to coordinate their actions, and they can often do so using guarded blocks. Such a block begins by polling  a condition that must be true before the block can proceed. 

Suppose you have this method which has a shared variable `joy` which is altered by another thread. Having a while loop is good, but is wasteful since it executed continuously while waiting:

```java
public void guardedJoy() {
    while(!joy) {
        //
    }
}
```

A more efficient guard uses the `wait()` method which does not return until another thread has issued a notifcation that some special event may have occurred, which could be the event that the thread is waiting for.

```java
public synchronized void guardedJoy() {
    while(!joy) {
        try {
            wait();
        } catch (InterruptedException e) {}
    }
}
```

When wait is invoked, the thread releases the lock and suspends execution. At some future time, another thread will acquire the same lock and invoke `notifyAll()`, informing all threads waiting on that lock that something important has happened.

```java
public syncrhonized notifyJoy() {
	joy = true;
    notifyAll();
}
```

