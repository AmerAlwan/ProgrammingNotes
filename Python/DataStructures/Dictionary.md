# Dictionary

A collection that is unordered and mutable (can be updated)

### Creating Dictionary

```python
data = {
    "key1" : "value1",
    "key2" : "value2"
}
```

### Accessing Data

#### Checking If Key Exists

```python
if "key1" in data.keys():
    print(True)
else:
    print(False)
```

#### Square Brackets

This method is easier to read but if you try accessing a `None` (null) key, it will return an error

```python
data["key1"] 
```

#### Get Method

This method will return `None` if you try accessing a null variable

```python
data.get("key1")
```

### Updating/Adding Data

To update or add a key, use square brackets

```python
data["key1"] = "key1New"
```

### Removing  Data

Use the `pop` method

```python
data.pop("key1")
```

The `del` keyword can also be used

```python
del data['key1']
```

### Printing Data

#### Using Print

```python
print(data)
```

#### Using For Loop

```python
for i in data.keys():
    print(i, data[i])
```

#### Using For Loop #2

```python
for key, value in data.items():
    print(key, value)
```

