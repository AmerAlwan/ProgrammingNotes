# List & Forward_List

> `forward_list` is singly linked list while `list` is doubly linked list

Lists are sequence containers with non-contagious memory allocation.

### Making a List

``` cpp
list<int> lst;
forward_list<int> fwdlst;
```

### Iterating through List

``` cpp
forlist<int>::iterator it = lst.begin(); it != lst.end(); ++it) {
    cout << *it << endl;
}
```

### Inserting Elements

#### At beginning

```cpp
lst.push_front(1);
```

#### At end

```cpp
lst.push_back(1);
```

#### At Index

To insert an element at a certain index, create an iterator, then point it to the index you want to insert the element at using the `advance` function. Then use the `insert` function to insert the new element at the iterator's position

```c++
list<int>::iterator it = lst.begin();
//Makes iterator point to 3rd position
advance(it, 2);
//Inserts 5 at 3rd position
lst.insert(it, 5);
```

#### Multiple Elements with Replacing

The `assign` function inserts `n`occurences of an element starting from the beginning of the list. If there are already elements in the list, it will replace them

```cpp
//Creates 3 occurences of '2'
lst.assign(3,2);
```

#### Multiple Elements at Index

The `insert` function with 3 parameters will insert n occurrences of an elements starting from where the iterator is pointed

```cpp
//Inserts 2 occurences of 7 at 4th position
advance(it, 3);
lst.insert(it,2,7);
```

### Removing Elements

#### At beginning

```cpp
lst.pop_front();
```

#### At End

```cpp
lst.pop_back();
```

#### At Index

```cpp
list<int>::iterator it = lst.begin();
//Points iterator to 3rd element
advance(it, 2);
//Removes 3rd element
lst.erase(it);
```

#### Certain Range

Create two iterators, one pointing to the first element, and another pointing to the last element

```cpp
list<int>::iterator itFirst = lst.begin();
list<int>::iterator itLast = lst.end();
lst.erase(itFirst, itLast);
```

#### All Elements with Certain Value

```cpp
lst.remove(val);
```

#### All Elements

```cpp
lst.clear();
```

