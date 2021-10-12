# Threads

Although threads in python appear to run multiple processes at once, each process does not use a separate processor/core. In order to actually run multiple tasks simultaneously, `multiprocessing` will have to be used which comes with some overhead.

The Python standard library provides `threading` which is used to create threads.

```python
import threading
```

## Creating and Running Threads

### Creating a Thread

To create a thread, you use the `threading` framework and the `Thread` function. 

When you create a thread, you pass it a function and a list containing the arguments to that function.

```python
import time
def thread_func(name):
    print("Hello " + name)
    time.sleep(2)
    print("Finished")
print("Before Running Thread")
x = threading.Thread(target=thread_func, args = ("Bob",))
```

### Starting a Thread

To start a thread, use the `start()` function

```python
x.start()
print("During Running Thread")
```

The output for the program is:

```python
# >> Before Running Thread
# >> Hello Bob
# >> During Running Thread
# >> Finished
```

## Thread Types

### Daemon Threads

A daemon thread in Python is a thread that will shut down immediately when the program exits. 

When using non-daemon threads, the program will wait for those threads to complete before terminating. Threads that are daemons are just killed wherever they are when the program is exiting

#### Declaring a daemon Thread

To declare a thread as daemon, add the `daemon` argument in the `Thread` function;s parameter and set it to true

```python
x = threading.Thread(target=thread_func, args=("Hello",), daemon=True)
```

Now, when running the program, the output will be:

```python
# >> Before Running Thread
# >> Hello Bob
# >> During Running Thread
```

The final line, "Finished", is missing because `thread_func()` did not get a change to complete as it was killed when `__main__` reached the end of its code.

### Joining Threads

If a thread is joined using `join()`, then the main thread will pause and wait for the thread to complete running.

```python
x.join()
```

The output of the program will then be:

```python
# >> Before Running Thread
# >> Hello Bob
# >> Finished
# >> During Running Thread
```
