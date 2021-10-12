# Threads

## What are Threads

**Process: ** A process is a program in execution. A process is managed by a Kernel. When a process runs, the operating system has to give it a lot of resources including memory. // A unit of activity characterized by a sequence of instructions, a current state and an associated set of system resources.

**Thread: ** is also called a lightweight process. It is not fully a process, but is part of the a process. A running program will have at least one thread running.  // A path of execution in a process characterized by an execution state, execution stack and local variables.

Multi threading has become important lately because of hardware. Processors today have reached their speed limitations, as in their speed can not be bumped because it is limited by the speed of electrons. Therefore, today computers divide processors into multiple cores. Therefore, in order to utilize the full efficiency of a processor, you have to write multi threaded programs.

### Multi-tasking vs Multi-processing

Previously, when running multi-threaded programs, they were all running on the same processor, creating only an illusion. There was an algorithm that would divide the total time into chunks and gives each thread its own chunk of time.

If there are multi processor or cores, you can actually have multiple threads running at once. This is why you multi threading is more important as you can actually utilize the full potential of hardware.

### What is "Thread Safe" and Race Conditions

An object that is thread safe is one that can function in a multi-threaded environment without having any **race conditions**.

**Race Conditions: **Unpredictable results due to rouge threads (run in unpredictable order)

## Operation

### Starting a thread

Conceptually, there are two ways of starting a thread in `Java`:

1. Writing a class a that inherits from the thread class. 
   The problem with this is that if you have other parent classes, then you cannot do that as you cannot extend from multiple classes at once.

   ```java
   class Runner extends Thread {
       public void run() {
           //Code Here
       }
   }
   public class Test {
       public static void main(String[] args) {
           Runner runner1 = new Runner();
           runner1.start();
       }
   }
   ```
   
   
   
2. Writing a class that implements the runnable interface that has a `run()` method which you have to override. Then you declare a thread and input the runnable as a parameter. To start the thread, do `thread.start()` and not `thread.run()`. You do this because the `start()` method will start the thread and then run the `run()` method while calling the `run()` method directly will run it int he current process.

   ```java
   //Method 1 >>>>>>>>>>>
   Runnable runnable = () -> {
       //Code Here
   };
   Thread t = new Thread(runnable);
   t.start();
   //Method 2 >>>>>>>>>>>
   Thread t = new Thread(() - > {
       //Code Here
   });
   t.start();
   //Method 3 >>>>>>>>>>>
   class Runner implements Runnable {
       public void run() {
           //Code Here
       }
   }
   public class Test {
       public static void main(String[] args) {
           Runner t1 = new Thread(new Runner());
           t1.start();
       }
   }
   ```

**Disclaimer: ** You have to start a thread with `start()`. If you call `run()`, it will run the method in the current/main thread while the `start()` method will run the `run()` method in a new thread.

### Joining a Thread

If you want to wait for a thread to finish, you join it using `thread.join()`.

This command will:

* Block the caller
* Wait for the thread to finish
* Returns when the thread is done

## Problems

The one big problem with multi-threading is coordination. It is similar to the term "Too many cooks spoil the broth". If you have too many cooks, then two of them could add salt thinking the other did not, and now you have a salty broth. 

### Critical Section

A critical section of a code is one where multiple threads try to modify code, but could interfere with each other in a way that messes up that code or causes an error. If you have multiple threads and each one is only reading a variable, then there is no problem. However, if even one of those threads is changing that variable, 

#### Example

```
variable: C
Thread 1 {
	//This is a critical section as variable c is being changed
	C++
}
Thread 2 {
	//This is a critical section as variable c is being changed
	C++:
}
```

In the above example, what happens is:

1. **Thread 1:** reads value of C into its own temporary memory : C = 10
2. **Thread 2:** reads value of C into its own temporary memory : C = 10
3. **Thread 1: ** Increases the value by 1 in a separate memory : C++ = 11
4. **Thread 2: ** Increases the value by 1 in a separate memory : C++ = 11;
5. **Thread 1: **Wrote back the increased memory to C : C <-- 11
6. **Thread 2: ** Wrote back the increased memory to C : C <-- 11

**Dirty Read: **When you read some value and someone else reads the same value. After you read it, someone else changes that value. That reading becomes a dirty read because the value changed after you read it.

**Atomic: **Doing an operation in a single step without anything interfering

