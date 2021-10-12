# Class

To define a class, we use the keyword `class`

```python
class Test:
    pass
```

## Methods

### Creating Method

```python
class Car:
    def engine(self):
        print("Engine")
```

### Calling Methods of Classes

```python
Car().engine()
```

## Objects

### Declaring and Initializing

```python
toyota = Car()
```

## Constructor

The constructor method of a class has the name `__init__`

```python
class Car:
    def __init__(self, model):
        self.model = model
```

## Self

`self` represents the instance of a class. By using the `self` keyword we can access the data initialized in the constructor and methods of a class

```python
class Car: 
  def __init__(self, model): 
    self.model = model
  def brand(self): 
    print(self.model)  

car = Car("Bmw")
car.brand() # >> Bmw

```

## Class Variables

Variables that are declared outside of any method inside the class. These variables are related to the class itself rather to each object, and therefore can only be accessed by reverencing the class or an instance of the class

```python
class Car:
    type = "Honda"
    def __init__(self, model):
        self.model = model
	def brand(self):
        print(Car.type, self.model)
car = Car()
print(car.type)
```

