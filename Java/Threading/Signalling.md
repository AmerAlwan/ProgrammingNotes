# Signaling Mechanism

Signaling is useful in multithreading as it enables threads to send signals to each other. Therefore, threads can wait for signals from another threat indicating that data is ready to be processed.

## Condition variables

## Monitoring

Java monitor is an object of a class with `synchronized` methods, which can be invoked by one thread at a time. 

**!** Each monitor has an implicit **monitor lock** and **condition variable** (wait set)

**Condition Variables: ** Include the methods `wait()`, `notify()`, and `notifyAll()`, which are in scope of a `synchronized` method; A Signal-and-Continue policy is maintains through `notify()` and `notifyAll()`.

### Synchronized Method Example

```java
public class Queue<T> {
    int head = 0, tail = 0;
    T[QSIZE] items;
   	public synchronized T deq() {
        while(tail - head == 0) 
            this.wait();
        T result = items[head % QSIZE];
        head++;
        this.notifyAll();
        return result
    }
}
```

1. `public synchronized T deq() {`: The `synchronized` keyword will lock the monitor on entry and unlock on return
2. `this.wait();`: Will wait on implicit condition
3. `this.notifyAll()`: Will signal all threads waiting on condition

## Semaphores



