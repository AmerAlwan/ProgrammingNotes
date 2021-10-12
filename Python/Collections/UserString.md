# UserString

A string like container that acts as a wrapper around string objects and is used to create a string with modified or additional functionality

```python
from collections import UserString
```

## Implementation

```python
class MyString(UserString):
    def append(self, s):
        self.data += s
	def remove(self, s):
        self.data = self.data.replace(s, "")
        
s = MyString("string")
s.append("s") # >> strings
s.remove("r") # >> stings
```

