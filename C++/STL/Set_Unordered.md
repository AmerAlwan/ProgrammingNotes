# Set

> A *C++* `set` is equivalent to a *java* `TreeSet` 

Sets are containers that store unique elements in a specific order. The elements are `const`, and so cannot be modified once in the set.

A set will store elements in a balanced binary tree and in sorted order using the `<` operator unless another sorting criteria is specified.

### Creating Set

```c++
set<int> st {1,2,3,4};
```

### Creating Set (TreeSet) from Vector

```cpp
//vec = {1,2,3,4,5}
set<int> st(vec.begin(), vec.end());
```

### Iterating  Through Set

There are two methods which are important for iterating through a set:

- **begin():** Returns an iterator to the first element in the set
- **end():** Returns an iterator to the last element in the set

The `iterator` in C++ points to each element in the set

#### Iterating Through Set with `while` loop

```c++
set<int>::iterator it = st.begin();
while(it != st.end()) {
    //Since the iterator it is a pointer, you must inclue * so it would print the actual value
    cout << *it;
    ++it;
}
```

#### Iterating Through Set with `for` loop

```c++
for(set<int>::iterator it = st.begin(); it != st.end(); ++it) {
    cout << *it;
}
```

### Inserting Element into Set

```c++
st.insert(1);
```

### Erasing Element from Set

#### Using Element's Value

```c++
//st = {1,3,6,9}
st.erase(3);
//st = {1,6,9}
```

#### Using Pointer & Iterator

```c++
//st = {1,3,6,9}
set<int>::iterator it = st.begin();
it++;
st.erase(it);
//st = {1,6,9}
```

### Finding Element

The function used is `find`, which returns an `iterator` pointing to the element. If the element is not found, it will return an `iterator` pointing to `st.end()`.

```c++
//st = {1,3,6,9}
set<int>::iterator it =st.find(3);
if(it != st.end()) 
    cout << "Found";
else 
    cout << "Not Found";

```

# Multi Set

# Unordered Set

> `unordered_set` is the equivalent of `HashSet` in Java

Container that stores unique elements in no particular order. Since an unordered set is stored using a has table, it allows for fast retrieval of individual elements based on their value.

> A set has a time complexity of O(log n) while unordered_set has O(1)

### Creating Unordered_Set

```c++
unordered_set<int> unst {1,3,6,9};
```

# Unordered Multi Set







