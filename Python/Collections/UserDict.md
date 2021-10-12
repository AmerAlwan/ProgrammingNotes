# UserDict

Is a dictionary-like container that acts as a wrapper around the dictionary objects. It is used when creating a dictionary with some modified or new functionality.

```python
from collections import UserDict
```

## Implementation

### UserDict where deletion is not allowed

```python
class MyDict(UserDict):
    #__del__ is like a deconstructor
    def __del__(self):
        raise RuntimeError("Deletion not allowed")
	def pop(self, s = None):
                raise RuntimeError("Deletion not allowed")
	def popitem(self, s = None):
                raise RuntimeError("Deletion not allowed")
```

