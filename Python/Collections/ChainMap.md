# ChainMap

Encapsulates many dictionaries into a single unit and returns a list of dictionaries

```python
from collections import ChainMap
```

## Declaring ChainMap

```python
d1 = {1 : 2, 2 : 3}
d2 = {3 : 4, 4 : 5}
d3 = {5 : 6, 6 : 7}
c = ChainMap(d1, d2, d3) # >> ChainMap({1: 2, 2: 3}, {3: 4, 4: 5}, {5: 6, 6: 7})
```

## Accessing Elements

You can access any key from any dictionary in the `ChainMap` just like you would with a normal dictionary

### Square Brackets

```python
c[1] # >> 2
c[6] # >> 7
```

### Values

```python
c.values() # >> ValuesView(ChainMap( {1 : 2, 2 : 3}, {3 : 4, 4 : 5}, {5 : 6, 6 : 7}))
```

### Keys

```python
c.keys() # >> KeysView(ChainMap( {1 : 2, 2 : 3}, {3 : 4, 4 : 5}, {5 : 6, 6 : 7}))
```

## Adding Dictionaries

To add a new dictionary, use the `new_child()` method. The new dictionary will be added at the beginning of the `ChainMap`. However, the dictionary has to be added into a new `ChainMap`

```python
d4 = {7 : 8, 8 : 9}
c1 = c.new_child(d4) # >> ChainMap({7 : 8, 8 : 9}, {1: 2, 2: 3}, {3: 4, 4: 5}, {5: 6, 6: 7})
```





