# Deque

Double Ended Queue. `Deque` is the optimized list for quicker append and pop operations from both sides of the container and provides O(1) time complexity whereas a list has O(n) time complexity

```python
from collections import deque
```

## Declaring Deque

```python
queue = deque([1,2,3]) # >> deque([1,2,3])
```

## Inserting Elements

### To Right

```python
queue.append(4) # >> 1,2,3,4
```

### To Left

```python
queue.appendleft(4) # >> 4,1,2,3
```

## Removing Elements

### To Right

```python
queue.pop() # 1,2
```

### To Left

```python
queue.popleft() # 2,3
```

