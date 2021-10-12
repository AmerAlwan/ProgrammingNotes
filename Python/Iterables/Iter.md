# Iter

The `iter()` function returns and iterator for the given object. It creates an object which can be iterated one element at a time.

```python
iter(obj, sentinel)
```

**object:** Object whos iterator has to be created

**sentinel (optional): **Special value that is used to represent the end of a sequence. The `iter()` function will return an iterator until the sentinel character isn't found

## Implementation

```python
nums = iter([1,2,3])
print(next(nums)) # >> 1
print(next(nums)) # >> 2
print(next(nums)) # >> 3
```

### Iterating until no values

```python
nums = iter([1,2,3])
while True:
    val = next(nums, None)
    if(val is None):
        break
	print(val)
# >> 1 .. 2 .. 3
```

### Custom Objects

For this example, we will create an iterator object that iterates to an inputted number

```python
class PrintNumber:
    def __init__(self, num):
        self.num = num
	def __iter__(self):
        self.count = 0
        return self
    def __next__(self):
        if(self.count >= self.num):
            raise StopIteration
		self.count += 1
        return self.num
printNum = iter(PrintNumber(2))
print(next(printNum)) # >> 1
print(next(printNum)) # >> 2
print(next(printNum)) # >> Stop Iteration Error
```