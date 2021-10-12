# Inheritance

The class from which properties are inherited is called the base class. The class which inherits the property of another class is called the derived class.

The syntax for a derived class is:

```python
class DerivedClassName(BaseClassName):
    pass
```

For the purposes of this note, our parent class will be `Vehicle`

Vehicle Class:

```python
class Vehicle:
    def __init__(self, name, color = 'Silver'):
        self.name = name
        self.color = color
	def get_name(self):
        return self.name
    def get_color(self):
        return self.color
```

## Creating Inheritance

```python
class Car(Vehicle):
    pass
```

## Inheritance Actions

### Overriding Methods

To override a parent method, simply recreate it in the child class

```python
class Car(Vehicle):
    def get_color(self):
        pass
```

### Using Variables from Parent Class

You can use `self` variables from the parent class

```python
class Car(Vehicle):
    def get_color(self):
        self.color = "Black"
        return self.color
```

## Super

`super()` returns a temporary object of the superclass that then allows us to call that superclass's methods.

```python
class Car(Vehicle):
    def __init__(self, name, color):
        super().__init__(name, color)
	def get_description(self):
        return "Name: " + self.get_name() + ". Color: " + self.get_color()
```

Ex:

```python
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width
	def get_area(self):
        return self.length * self.width
class Square(Rectangle):
    def __init__(self, length):
        super().__init__(length, length)
```

## Multiple Inheritance

Example of the Car class inheriting from two parents, the `Vehicle` and `Cost` classes

```python
class Cost:		
    def __init__(self, cost):
        self.cost = cost
    def get_cost(self):
        return self.cost
class Car(Vehicle, Cost):
    def __init__(self, brand_name, model, cost): 
        self.model = model 
        Vehicle.__init__(self, brand_name) 
        Cost.__init__(self, cost) 
    def get_description(self):
        return self.get_brand_name() + self.model + " is the car " + "and it's cost is " + self.get_cost()
```

Note how instead of using `super()`, each class's constructor is called by writing the actual name of the class as `Vehicle.__init__` and `Cost.__init__`