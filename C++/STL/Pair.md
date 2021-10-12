# Pair

Used when you want a pair of values of any type.

## Creating pair

### Creating Pair by Initialization

```cpp
pair<int, double> p = {1,2d};
```

### Creating Pair with `make_pair`

```cpp
pair<int, double> p;
p = make_pair(1, 2d);
```

## Displaying Pair

### Whole Pair

```cpp
cout << p;
```

### Individual Values

```cpp
cout << p.first + " " + p.second;
```

