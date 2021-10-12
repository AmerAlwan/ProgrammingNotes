# Multithreading

The way to create multiple threads is the same as a single thread using `threading.Thread()`. The hard way of doing it is:

```python
import threading, time

def thread_func(name):
    print("Thread ", name)
    time.sleep(2)
    print("Finished")
    
threads = list()

for index in range(3):
    print("Created Thread ", index)
    x = threading.Thread(target=thread_func,args=(index,))
    threads.append(x)
    x.start()

for index, thread in enumerate(threads):
    print("Before Joining Thread ", index)
    thread.join()
    print("After Joining Thread ", index)
```

The output of the program would be:

```
Created Thread  0
Thread  0
Created Thread  1
Thread  1
Created Thread  2
Thread  2
Before Joining Thread  0
Finished Thread  1
Finished Thread  0
After Joining Thread  0
Before Joining Thread  1
Finished Thread  2
After Joining Thread  1
Before Joining Thread  2
After Joining Thread  2
```

## Thread Pool Executor

An easier and cleaner way to start up a group of threads is by using a `ThreadPoolExecutor`. 

```python
from concurrent.future import ThreadPoolExecutor
```

### Creating  a TPE

```python
executor = ThreadPoolExecutor(max_workers=3)
```

### Submit

In order to give threads within the TPE, we use the `submit()` function and pass in the function as the parameter

```python
executor.submit(thread_func(1))
```

### Map

The `map()` allows multiple calls to a provided function, passing each of the items in an `iterable` to that function. Except, the functions are called concurrently.

```python
executor.map(thread_func, range(3))
```

The first parameter is the function to call. The second parameter is a list or tuple containing the arguments for the parameters of the function. The amount of concurrent threads that will start depends on the number of variables in the list or tuple. 

Ex:

```python
executor.map(thread_func, ("a","b","c"))
# >> Thread a
# >> Thread b
# >> Thread c
```

```python
def thread_func(name, num):
    print("Thread ", name, num)
executor.map(thread_func, ("a","b"), (1,2))
# >> Thread a 1
# >> Thread b 2
```

### Context Manager

The easiest way and most common way to create a TPE is a context manger, using the `with` statement to manage the creation and destruction of the pool

The TPE can be imported from the standard Python library `conurrent.futures`

```python
with ThreadPoolExecutor(max_workers=3) as executor:
    executor.map(thread_func, range(3))
```

The code creates a TPE as a context manager, and tells it how many threads are in the pool. The `map()` method is used to step through an `iterable` of things, which in this case is `range(3)`, passing each one to a thread in the pool.

The output for the code is:

```
Thread 1
Thread 2
Thread 3
```

#### What does Context Manager do?

In the context manager, the `with` statement is blocking. It essentially joins all threads to the main program and blocks there until all threads have completed processing.

##### Ex Without Context Manager

```python
executor = ThreadPoolExecutor(3)
executor.map(thread_func, range(3))
print("Main")
```

The Output is:

```
Main
Thread 0
Thread 1
Thread 2
```

##### Ex With Context Manager

```python
with ThreadPoolExecutor(3) as executor:
    executor.map(thread_func, range(3))
print("Main")
```

The equivalent of the above code can be written without a Context Manager as:

```python
executor = ThreadPoolExecutor(3)
executor.map(thread_func, range(3))
executor.shutdown(wait=True)
print("Main")
```

The Output is:

```
Thread 0
Thread 1
Thread 2
Main
```

### Examples

#### Is Number Even

```python
def isEven(num):
    return True if num % 2 == 0 else False
nums = [1,2,3,5,7,10,100]
with ThreadPoolExecutor(3) as executor:
    for num, isEven in zip(nums, executor.map(isEven, nums)):
        if isEven:
            print(num, "is even")
		else:
            print(num, "is odd")
```

Output:

```
1 is odd
2 is even
3 is odd
5 is odd
7 is odd
10 is even
100 is even
```

