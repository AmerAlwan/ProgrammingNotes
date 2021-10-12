# Functions and Arguments

## Declaring Functions

### Known Parameters

```python
def func():
    print("Test")
def func2(test):
    print(test)
```

### Unknown Arguments

If you do not know the number of arguments being passed in, you can put a `*` before the variable name

```python
def add(*num):
    print(num)
```

Ex:

```python
def add(*num):
    print(sum(num))
add(1,2) # >> 3
add(1,2,3) # >> 6
add(1, 1.5) # >> 2.5
```

#### Unpacking tuple

Just like you can pass many variables into a function and turn them into a tuple, you can also pass a tuple into a function and turn it into individual variables

```python
def add(a, b):
    print(sum(a,b))
t = (1,2)
add(*t) # >> 3
```

### Unknown Order

There are times that we do not know the order in which the parameters will be passed in. For example, say that a function accepts two parameters, `name` and `age`. You want to print the name followed by the age, but you cannot guarantee that the first parameter inputted will be the name or age.

```python
def user(name, age):
    print(name, age)
user("Amer" 18) # >> Amer 18
user(10, "Amer") # >> 18 Amer
```

One method to combat this is using the keyword arguments when calling the function

```python
user(age = 18, name = "Amer") # >> Amer 18
```

### Default Argument

In python, you can initialize a default value for a variable declared in the parameter of a function

```python
def user(name, age = None):
    print(name, age)
user("Amer") # >> Amer None
user("Amer", 18) # >> Amer 18
```

> **Remember: **All compulsory arguments must be declared first and then the default argument must be declared
>
> Accepted:
>
> ```python
> def user(name, age = None)
> ```
>
> Not Accepted: 
>
> ```python
> def user(name = None, age)
> ```
>
> Not Accepted:
>
> ```python
> def user(name = None, age, height = 0)
> ```
>
> 

### Unknown Keyword Arguments (Kwargs)

By putting a `**` in front of the parameter variable, you are essentially passing a dictionary of arguments and can therefore access and modify variables passed into the parameter

```python
def user(**details):
	print(details)
    
user(name = "Amer", age = 18) # >> {'name': 'Amer', 'age': 18}
```

You can also access and modify the variables

```python
def user(**details):
	print(details["name"])
    
user(name = "Amer", age = 18) # >> Amer
```

### Functions as Parameters

In python, you can also pass functions into another function's parameters just as if they were an object or a primitive data type.

```python
def hello(name):
	return "Hello " + name
def hello_bob(hello_func):
    return hello_func("Bob")
hello_bob(hello) # >> Hello Bob
```

## Inner Functions

It is possible to define functions inside other functions, which are called Inner Functions

```python
def parent():
    print("Parent")
    def first_child():
        print("First Child")
	def second_child():
        print("Second Child")
	second_child()
    first_child()
parent()
# >> Parent
# >> Second Child
# >> First Child
```

The inner functions are not defined until the parent function is called. They are locally scoped to `parent()` and therefore exist only inside the `parent()` function as local variables.

## Returning Functions

Python also using functions as return values

```python
def parent(num):
    def first_child():
		return "First Child"
	def second_child():
        return "Second Child"
    if num == 1:
        return first_child
    else:
        return second_child
    
```

In this example, since the functions are returned without parenthesis, that only the function reference is returned.

```python
first = parent(1)
# >> <function parent.<locals>.first_child at 0x7f599f1e2e18>
second = parent(2)
# >> <function parent.<locals>.second_child at 0x7f599dad5268>
```

Since `first` and `second` are referring to the inner functions, they can be used as regular functions, even though the functions they point to can't be accessed directly

```python
first()
# >> First Child
second()
# >> Second Child
```

