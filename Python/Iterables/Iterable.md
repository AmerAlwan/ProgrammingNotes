# Iterable

An `iterable` in python is any Python object capable of returning its members one at a time, permitting it to be iterated over in a `For` loop. 

These include `List`, `Tuple`, `String`, `Set`, `Dict`.  

In reality, an `iterable` is any object with an `__iter__()` method or with a `__getitem__()` method that implements the `Sequence` semantics.

## Functions

There are various functions that accept an `iterable` and act on it

### Sum

Returns the sum of contents

### Sorted

Return a list of the sorted contents of an `iterable`

### Any

Returns `True` and ends the iteration immediately if `Bool(item)` was `True` for any item in the `iterable`

```python
any((0, None, [], 0, 'X', -1, True)) # >> True
```

### All

Returns `True` inly if `bool(item)` was `True` for all items in the `iterable`

```python
all([1, (0,1), True, "hi"]) # >> True
```

### Max

Returns the largest value 

### Min

Returns the smallest value

## Unpacking Iterables

If you want to store the values in a list into individual variables, we can use `iterable` unpacking.

### Implementation

#### Using Variables

A typical way to store values in a list into individual variables would be:

```python
arr = [1,2,3]
a = arr[0]
b = arr[1]
c = arr[2]
```

Using unpacking, we can shorten this code and make it simpler and easier to read

```python
arr = [1,2,3]
a,b,c = arr
# >> a = 1, b = 2, c = 3
```

#### Using For Loop

Unpacking can be used in For loops when iterating through `iterables` within `iterables`, where  each value within the inner `iterable` is assigned its own variable as you iterate through the list

 ```python
nums = [(1,2),(2,3),(3,4)]
for num1, num2 in nums:
    print(num1, num2) # >> 1 2, 2 3, 3 4
 ```

### Unpacking Huge Iterables

What if you want to unpack a list with hundreds of values. Using individual variables in this case is inefficient. Instead, you can use one variable with a `*` before it. This would unpack the `iterable` into a list

#### Implementation

```python
l = range(10)
*a, = l
# >> [0,1,2,3,4,5,6,7,8,9]
```

#### Purpose

Many algorithms would require you to split a sequence in a "first, rest" pair.

```python
seq = range(10)
first, *rest = seq
# >> 0
# >> [1,2,3,4,5,6,7,8,9]
```

You can have as many individual variables as you want, and any leftover variables will be assigned to the variable with a `*` before it. Be careful to ensure that there are enough variables in the list though.

```python
a, *b, c = range(5)
# >> a = 0
# >> b = [1, 2, 3] 
# >> c = 4
```

#### In For Loops

```python
for a, *b in [(1,2,3), (4,5,6,7)]:
	pass
# >> a -> 1, 4
# >> b -> (2,3), (5,6,7)
```

## Enumerating Iterables

The built in `enumerating` function allows us to iterate over an `iterable` while keeping track of the iteration count.

The `enumerate` function accepts an `iterable` as an input, and returns a new `iterable` that produces a tuple of the iteration count and the corresponding item from the original `iterable`. 

```python
for entry in enumerate("abcd"):
    print(entry)
# >> (0, 'a'), (1, 'b'), (2, 'c'), (3, 'd')
```

### Example - Where value is None

Say you have an `iterable` and you want the indices where the value is `None`. Typically, you would do this as follows:

```python
none_indices = []
index = 0
for item in [2, None, -10, None, 4, 8]:
    if item is None:
        none_indices.append(index)
	index += 1;
# >> [1, 3]
```

However, with the `enumerate` function, this can be shortened and some variables can be eliminated

```python
none_indices = []
for index, item in enumerate([2, None, -10, None, 4, 8]):
    if item is None:
        none_indices.append(index)
# >> [1,3]
```

### Example - Unsorted Index

In this example, we will be creating a function that returns the index where the value in an `iterable` is unsorted. If the `iterable` is all sorted, then it will print "Sorted".

```python
my_list = [1,4,5,6,7,4,3,5,6,0]
prev = None
for index, item in enumerate(my_list):
    if index != 0 and prev > item:
        print(index)
        break
    prev = item
else:
    print("Sorted!")
```

