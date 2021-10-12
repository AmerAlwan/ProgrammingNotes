# Counter

A counter is a subclass of dictionary. It is like a hash table as in it holds the data in an unordered collection and allows you to count the items in an inerrable list. 

The elements in a counter represent the keys and the count as values.

```python
from collections import Counter
```

## Declaring Counter

There are multiple forms to declare a counter.

### Sequence of Items

```python
Counter(['B', 'B', 'A', 'B', 'C', 'A', 'B', 'B', 'A', 'C'])
# >> Counter({'B' : 5, 'A' : 3, 'C' : 2})
```

### Dictionary

```python
Counter({'B' : 5, 'A' : 3, 'C' : 2})
# >> Counter({'B' : 5, 'A' : 3, 'C' : 2})
```

### Keyword Arguments

```python
Counter(A=3, B=5, C=2)
# >> Counter({'B' : 5, 'A' : 3, 'C' : 2})
```

## Example

```python
from collections import Counter

arr = [1,1,1,5,3,1,5,6,7,6,7,6,5,4]

count = Counter(arr)

print(count[1]) # >> 4
```

