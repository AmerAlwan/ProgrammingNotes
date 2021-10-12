# OrderedDict

A subclass of dictionary that remembers the order in which keys were inserted

```python
from collections import OrderedDict
```

### Declaring OrderedDict

```python
od = OrderedDict()
od[1] = 2
od[2] = 3
od[3] = 4
### OR
od = orderedDict({1 : 2, 2 : 3, 3 : 4})
```

### Maintaining Order

When deleting items from the `OrderedDict`, the order of insertion will still be maintained and all items shift one up. Any newly inserted item will also insert at the end of the list.

```python
od.pop(1)
od[1] = 2
# >> {2 : 3, 3 : 4, 1 : 2}
```

