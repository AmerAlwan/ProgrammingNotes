# Decorators

## Introduction

Decorators wrap a function, modifying its behavior.	

```python
def decorator(func):
    def wrapper():
        print "Before the func is called"
        func()
        print "After the func is called"
	return wrapper
def say_hello():
    print("Hello")
say_hello = decorator(say_hello)
say_hello()
# >> Before the func is called
# >> Hello
# >> After the func is called
```

### The '@' Symbol

The above example is very clunky, and requires `say_hello()` to be written 3 times. The `@` symbol ('pie' syntax) helps shorten the code.

```python
@decorator
def say_hello():
    print("Hello")
```

The `@decorator` is equivalent of saying `say_hello = decorator(say_hello)`

## Examples

### `@do_twice` decorator

```python
def do_twice(func):
    def wrapper():
        func()
        func()
	return wrapper
@do_twice
def say_hello():
    print("Hello")
say_hello()
# >> Hello
# >> Hello
```



## OLD NOTE

Decorators is a function that take a function and extends its functionality without modifying it explicitly.

First, we declare the decorator function and in the arguments of the function we expect the function to be passed as an argument. Inside that method, we write a wrapper function where operations are carried out and it is returned.

```python
def decorator(func):
    def wrapper():
        print("Line Number 1")
        func()
        print("Line Number 3")
	return wrapper

@decorator
def line2():
    print("Line Number 2")

line2()

# >> Line Number 1
# >> Line Number 2
# >> Line Number 3

@decorator
def middleLine():
    print("Middle Line")

middleLine()

# >> Line Number 1
# >> Middle Line
# >> Line Number 3
```



