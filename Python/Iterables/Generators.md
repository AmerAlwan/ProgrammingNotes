# Generators

Generators are a special kind of `iterable` which stores the instructions for how to generate each of its members, in order, along with is current iteration state, without having to store them all in memory at once.

For example, a list stores all its items and they can be accessed via indexing. A generator does not store any items, only the instructions for generating each of its members and its iteration state. The generator knows for example that is has generate its second member, and so it will generate its third member the next time it is iterated on.

The whole point of generators is to produce a long sequence of items without having to store them all in memory.

## Yield

The `yield` keyword will result in/ return a generator object. It is used instead of `return`, except the function will return a generator, or the state of the function. When `next()` is called on a generator object, the previously yielded variable is incremented, and then yielded again.

```python
def generator():
    for i in range(3):
        yield i*i
mygen = generator()
for i in mygen:
    print(i)
```

When you call `generator()`, the code in the function body does not run. Only the generator object is returned. Essentially, what is returned is the address for the instructions for the first operation of `i*i`. 

The code will continue from where it left off each time `for` uses the generator.

The first time the `for` calls the generator object created from the function, it will run the code in your function from the beginning until it hits yield, then it'll return the first value of the loop. Then, each subsequent call will run another iteration of the loop in the function and return the next value. This will continue until the generator is considered empty, which happens when the function runs without hitting `yield`.

### Example: Infinite Loop

You can easily create an infinite loop of adding 1 to a variable, but this would run you into a problem because memory is finite. You can therefore create a generator, which will run infinitely since memory is not being consumed

```python
def infinite_seq():
    num = 0
    while True:
        yield num
        num += 1
for i in infinite_seq():
    print(i)
0 .. 1 .. 2 .. 3 .. Infinity
```

This program will run until it is interrupted by the user

## Range Generator

```python
range(start, stop, step)
```

start: Included, default = 0

stop: excluded

step: By how many variables to iterate by in each iteration; Default = 1

```python
for i in range(1, 10, 2):
    print(i)
# >> 1 .. 3 .. 5 .. 7 .. 9

```

### Reverse Range

```python
for i in range(3,0,-1):
    print(i)
# >> 3 .. 2 .. 1
```



### Memory Consumption: Generators vs Lists

![Memory consumption figure](https://www.pythonlikeyoumeanit.com/_images/Mem_Consumption_Generator.png) 

## Generator Comprehensions (Custom Generators)

Generator Comprehension is python's syntax for defining a simple generator in a single line of code. 

The general form of generator comprehensions is

```python
(<expression> for <var> in <iterable> if <condition>)
```

In long form, this line would be:

```python
for <var> in <iterable>:
    if bool(<condition>):
        yield <expression>
```

### Example: Return Even Numbers

```python
gen = (i for i in range(100) if i % 2 == 0)
```

### Multiple Parameters

```python
((i, i**2, i**3) for i in range(3))
# >> (0,0, 0) .. (1,1,1) .. (2,4,8)
```

### With if and else

```python
((1 if i < 3 else 2) for i in range(6))
# >> 1 .. 1 .. 1 .. 2 .. 2 .. 2
```

## Storing Generators

Generators defined using comprehension also do not consume any memory. Therefore, if you create a generator and then try to access a value from that generator, you will be unable.

When attempting to print a generator, we are getting the memory address for the instructions for generating our sequence of squared numbers.

```python
gen = (i**2 for i in range(3))
print(gen)
# >> generator object <genexpr> at 0x000001E768FE8A40>
len(gen)
# >> TypeError: object of type 'generator' has no len()
gen[2]
# >> TypeError: 'generator' object is not subscriptable
```

### Viewing Generator Values

#### Without Memory Consumption

To view the values in the generator, you have to iterate through it using `iter()`, which will not consume any memory

```python
gen_iter = iter(gen)
while True:
    val = next(gen_iter)
    if(val == None):
    	break
```

You can also use a for loop:

```python
gen = (i for i in range(3))
for i in gen:
    print(i)
# >> 0 .. 1 .. 2
```

#### With Memory Consumption

To view the values with memory consumption, you can use functions like `list()`

```python
gen_list = list(gen)
print(gen_list)
```

## Consuming Generators

We can feed a generator into any function that accepts `iterables`. However, these functions will consume the generator, essentially leaving it exhausted and inaccessible afterwards as it is iterated over in full

```python
gen = (i for i in range(3))
sum(gen) # >> 3
# 'gen' has already been consumed. So the sum computes to nothing
sum(gen) # >> 0
```

Therefore, the generator must be redefined if it is to be iterated over again

## List & Tuple Comprehension

### List Comprehension

Generators can be used to initialize lists. Aside from the `list()` function, the generator can also be surrounded by `[]`

```python
words = ['Python', 'Like', 'You', 'Mean', 'It']
o_words = [word for word in words if "o" in word.lower()]
# >> ['Python', 'You']
```

#### Example: Translating a For-Loop

Given...

```python
out = []
for i in "Hello. How Are You?":
    if i.islower():
        out.append(1 if i == "o" else 0)
```

With Generators, it is written as:

```python
out = [(1 if i == 'o' else 0) for i in "Hello. How Are You?" if i.islower()]
# >> [0, 0, 0, 1, 1, 0, 0, 0, 1, 0]
```

### Tuple Comprehension

You can use the `tuple()` function to initialize a generator as a tuple

```python
tup = tuple(i for i in range(3))
# >> (0,1,2)
```

## Nesting Comprehension

You can use list comprehension to nest lists within lists, essentially creating a matrix

### Example: 3x4 Matrix

```python
matrix = [[0 for col in range(4)] for row in range(3)]
# >> [[0,0,0,0],[0,0,0,0],[0,0,0,0]]
```

