# Lists

A list is a data structure that allows you to group together multiple variables under one label. Unlike arrays in Java, lists in python can have values of different types

Ex: 

```python
data = [1, "Cat", True, 5.0]
```

### Accessing Elements

To access one element, you use square brackets

```python
print(data[0])
# >> 1
```

You can also access multiple data in a range in the list

```python
print(data[0:3])
# >> [1, "Cat", True]
```

### Adding Elements

To add elements, you use the `append` method

```python
data.append("Hello")
```

### Removing Elements

To remove elements, you use the `remove` method

```python
data.remove("Hello")
```

### Looping Through Elements

```python
for i in data:
    print(i)
```

### Check if element exists

```python
if 1 in data:
    print(True)
```

### Checking Length

```python
len(data)
```

