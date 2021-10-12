# Locks & Conditions

Synchronization is built around `intrinsic locks` or `monitor locks`. Locks in java allow you to lock threads while awaiting for conditions. 

Every object has an intrinsic lock associated with it. A thread that needs exclusive and consistent access to an object's fields needs to acquire the object's intrinsic lock before accessing them, and then release the intrinsic lock when it's done with them. 

As long as a thread owns an intrinsic lock, no other thread can acquire the same lock. The other thread will block when it attempts t acquire the lock.

When a thread invokes the `synchronization` method , it automatically acquire the intrinsic lock for that method's object and releases it when the method returns.

When a thread releases an intrinsic lock, a happens-before relationship is established between that action and any subsequent acquisition of the same lock.

## Reentrant Lock

Represents a reentrant mutual exclusion lock which allows the creation of condition variables to wait for conditions.

Like synchronized objects, reentrant locks are monitors and allow blocking on a condition rather than spinning.

When acquiring a lock, you need to ensure that it is released or it could result in deadlock or another issue.

### Simple Lock Implementation

```java
Lock lock = new ReentrantLock();
lock.lock();
try {
    //Access the resource protected by this lock
} finally {
    lock.unlock();
}
```



## Condition Interface

A condition allows a thread to suspend its execution until the condition is true. A condition object is bound to a lock and can be obtained from the lock class by calling the `newCondition()`method.

A condition can have the effect of containing multiple wait-sets per object, by combining these sets with the use of a lock implementation. A condition must atomically release the associated lock and suspend the current thread's execution.

It allows one thread to suspend execution (to "wait") until notified by another thread. The suspended thread releases the lock

### Lock Methods

1. `void lock();`: Will acquire a lock
2. `boolean tryLock();`: Try for lock, but not too hard
3. `Condition = new Condition();`: Create condition to wait on

### Condition Methods

1. `await()` | `await(long time, TimeUnit unit`: Release lock and wait on condition

- Release lock associated with the object
- Sleeps (gives up processor)
- Awakens (resumes running) when signaled by `signal()` or `signalAll()`
- Reacquires lock & returns

2. `signal()`: Wake up one waiting thread

3. `signalAll()`: Wake up all waiting threads 

### Producer and Consumer

