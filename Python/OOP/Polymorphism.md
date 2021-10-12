# Polymorphism

Polymorphism means same function name (but different signatures) being uses for different types.

## With Functions

```python
def add(*var):
    return sum(var)
```

## With Class Methods

```python
class USA:
    def language(self):
        print("English")
class Egypt:
    def language(self):
        print("Egypt")
```

### Using for loop

```python
usa = USA()
egypt = Egypt()
for country in (usa, egypt):
    country.language()
```

### Using Function

```python
def func(obj):
    obj.language()
usa = USA()
egypt = Egypt()
func(usa)
func(egypt)
```

## With Inheritance

```python
class Country:
    def language(self):
        print("The international language is English, but not all countries speak it")
class USA(Country):
    def language(self):
        print("USA speaks English")
class Egypt(Country):
    def language(self):
        print("Egypt does not speak English")
	
```

