# DefaultDict

A subclass of dictionary that is used to provide some default values for the key that does not exist and never raises a `KeyError`

```python
from collections import defaultdict
```

## Declaring DefaultDict

When declaring the `defaultdict`, put the type that the dictionary will accept into the parameter. Therefore, the default value will be assigned based on the type

### Example with Int

```python
d = defaultdict(int)
for i in range(10):
    # Since the default dict's type is int, the default value of the dict will be 0. Instead of assigning 0 to every index, it is automatically assigned and so we can do this addition operator without the program crashing because the value has not been initialized
    d[i] += 1
```

### Example with List

```python
d = defaultdict(list)
for i in range(5):
    # In this case, each index of the dictionary will create a new empty list. In this for loop, we are simply appending a number to each of the empty lists
    d[i].append(i)
	# >> {0 : [0], 1 : [1], 2 : [2], 3 : [3], 4 : [4]}
```

