# UserList

Acts as a wrapper around the list objects and is useful for creating a list with some modified or additional functionality

```python
from collections import UserList
```

## Implementations

```python
class MyList(UserList):
    def remove(self, s = None):
                raise RuntimeError("Deletion not allowed")
	def pop(self, s = None):
                raise RuntimeError("Deletion not allowed")
            
l = MyList([1,2,3])
l.remove() # >> Deletion not allowed
```

