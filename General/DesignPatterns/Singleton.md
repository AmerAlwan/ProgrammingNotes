# Singleton

## Details

* Singleton patterns restricts the instantiation of a class and ensures that only one instance of the class exists in the java virtual machine
* The singleton class must provide a global access point to get the instance of the class
* Singleton patterns  is used for logging (keeping record of all data input/output, processes, final results, etc), drivers objects, caching and thread pool

## Implementation

- Have the class's constructor set to private
- Declare in the class a private static (or final) instance of the class
- Have a public static method that returns the instance of the class

### Eager & Static Block Initialization

In the eager approach, the instance of the class is created at the time of the class loading. The drawback to this method is that instance is created even though the client application might not be using it and this method does not provide any options for exception handling.

In addition, since the singleton is initialized once, you can declare it as final, which could help avoid some bugs.

```java
public class EagerSingleton {
    private static final EagerSingleton instance = new EagerSingleton();
    private EagerSingleton() {}
    public static EagerSingleton getInstance() { return instance; }
}
```

If you want to have exception handling, you can use a static block

```java
public class StaticBlockSingleton {
    private static StaticBlockSingleton instance;
    private StaticBlockSingleton() {}
    static {
        try {
            instance = new StaticBlockSingleton()
          	} catch(Exception e) {}
	}
}
```

### Lazy Initialization

Another approach is initializing the instance when the `getInstance()` method is called for the first time. 

However, this approach is not thread safe. If two threads call the method at the same time, both threads will get different instances of the singleton class, hence destroying the singleton pattern.

```java
public class LazySingleton {
    private static LazySingleton instance = null;
    private LazySingleton() {}
    public static LazySingleton getInstance() {
        if(instance == null) instance = new LazySingleton();
        return instance;
    }
}
```

### Thread Safe Lazy Initialization

This thread safe solution reduces the performance of the program because of the cost of having a synchronized method which will only allow one thread to access it at a time. 

```java
public class ThreadSafeSingleton {
    private static ThreadSafeSingleton instance = null;
    private ThreadSafeSingleton() {}
    public static synchronized ThreadSafeSingleton getInstance() {
        if(instance == null) instance = newThreadSafeSingleton();
        return instance;
    }
}
```

Since we only need synchronization for the first few threads which may initialize the singleton, we can use the `double checked locking` approach which has the synchronized block used inside the if condition with an additional check to ensure that only one instance of a singleton class is created

```java
public class ThreadSafeSingleton {
    private static ThreadSafeSingleton instance = null;
    private ThreadSafeSingleton() {}
    public static ThreadSafeSingleton getInstance() {
        if(instance == null) {
        	syncrhonized(ThreadSafeSingleton.class) {
                if(instance == null) instance = new ThreadSafeSingleton();
            }
        }
        return instance;
    }
}
```

### Enum Implementation

The safest and best implementation of a singleton is by creating it as an enum. This overcomes situations like Reflection because java always ensures that any enum value if instantiated once as well as that enums are globally accessible. 

```java
public enum EnumSingleton {
    INSTANCE;
    // Have Sinleton Variables and Methods Here
}
```

## Uses

- A reason someone could want to control how many instances a class has is if they want to control access to a shared resource. Ex: A database or a file
- A single database object is shared by different parts of the program
- Real World Analogy: A country can have only one official government. No matter the personal identities of the individuals who form governments, the government is a global point of access that identifies the group of people in charge



