# Queue

One-ended container that operates in FIFO (First in, first out)

### Creating Queue

```c++
queue <int> q;
```

### Inserting Elements

Adds element at end of queue

```c++
q.push(1);
```

### Removing Elements

Deletes first element in queue

```c++
q.pop();
```

### Getting First Element 

```c++
q.first();
```

### Getting Last Element

```c++
q.back();
```

# Deque

Double-ended queue that can expand and contract from both ends. They are similar to vectors but are more efficient at inserting and deleting elements. Deque also contains most of functions from `vector`.

### Creating Deque

```cpp
deque<int> dq;
```

### Front Operations

#### Adding Element

```cpp
dq.push_front(1);
```

#### Removing Element

```cpp
dq.pop_front(1);
```

### Back Operations

#### Adding Element

```cpp
dq.push_back(1);
```

#### Removing Element

```cpp
dq.pop_back(1);
```

### Finding Element  from Index

```
dq.at(2);
```



