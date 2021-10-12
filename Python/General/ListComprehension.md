# List Comprehension

Consider a situation where you want a list of squares. You can declares a squares list and then square a bunch of numbers in a for loop.

Ex: 

```python
squares = []
for x in range(10):
	squares.append(x**2)
```

With list comprehension, this can be achieved in a single line

## Single Set

There are two methods to accomplish this:

### Using Map and Lambda

```python
squares = list(map(lambda x : x ** 2, range(10)))
```

### Using For Loop

```python
squares = list(x**2 for x in range(10))
```

## Multiple Sets

If you want a list with a set of two numbers that are the same, we would write two for loops and one if condition

```python
num = list((i,j) for i in range(10) for j in range(10) if i == j)
# >> [(0, 0), (1, 1), (2, 2), (3, 3), (4, 4), (5, 5), (6, 6), (7, 7), (8, 8), (9, 9)]
```

