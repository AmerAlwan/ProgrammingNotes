# Encapsulation

Encapsulation is the prevention of data from being modified by accident

To make something private, add a `__` before the name

### Private Variable

```python
class Car:
    def __init__(self):
        self.__name = "Honda"
c = Car()
print(c.__name) # >> Gives error. Car has no attribute '__name'
```

### Private Method

```python
class Car:
    def __init__(self):
        self.name = "Honda"
	def __name(self):
        return self.name
c = Car()
print(c.__name()) # >> Gives error. Car has not attribute '__name'
```

## Accessing Private attributes/Methods

To access a private attribute of the class, start with an `_` followed by the class's name and then the attribute.

### Private Variable

```python
print(c._Car__name)
```

### Private Method

```python
print(c._Car__name())
```

