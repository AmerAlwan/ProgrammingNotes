# Locks & Conditions

Locks in java allow you to lock threads while awaiting for conditions

## Reentrant Lock

Represents a reentrant mutual exclusion lock which allows the creation of condition variables to wait for conditions.

Like synchronized objects, reentrant locks are monitors and allow blocking on a condition rather than spinning.

## Condition Interface

Represents a condition variable associated with a lock. 

It allows one thread to suspend execution (to "wait") until notified by another thread. The suspended thread releases the lock

## Example

### Java Lock Interface Example

```java
public interface Lock {
    void lock();
    void lockInterruptibly() throws InterruptedException;
    boolean tryLock();
    boolean tryLock(Long time, TimeUnit unit);
    Condition newCondition();
    void unlock;
}
```

1. `void lock();`: Will acquire a lock
2. `boolean tryLock();`: Try for lock, but not too hard
3. `Condition = new Condition();`: Create condition to wait on

### Java Lock Conditions Interface Example

```java
public interface Condition {
    void await();
    boolean await(long time, TimeUnit unit);
    void signal();
    void signalAll();
}
```

1. `await()`: Release lock and wait on condition
   - Release lock associated with the object
   - Sleeps (gives up processor)
   - Awakens (resumes running) when signaled by `signal()` or `signalAll()`
   - Reacquires lock & returns
2. `signal()`: Wake up one waiting thread
3. `signalAll()`: Wake up all waiting threads 