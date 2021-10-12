# Vector

## Creating a Vector

```cpp
vector<int> vec {1,2,3,4};
```

## Resize a Vector

The `resize(n)` method resizes the container so that it contains `n` elements. If `size > n` then then the back elements are removed. If `n > size` then extra elements are inserted at the back of the vector

## Iterating through Vector

### Iterating with Reference

In C++, the [] operator is overloaded with the vector class and will return a reference to an element based on the inputted key

```cpp
//vec = {1,2,3,4,5}
for(int i = 0; i < vec.size(); i++)
	cout << vec[i] << endl;
```

```cpp
//vec = {1,2,3,4,5}
for(int i = 0; i < vec.size(); i++)
	cout << vec.at(i) << endl;
```

### Iterating with Pointer

Another way you can iterate is using pointers. Just declare a pointer variable and initialize it by using the reference symbol `&` and then retrieving the variable in the vector by referencing to it

```c++
int *p = &vec[0];
for(int i = 0; i < vec.size(); i++) {
    cout << *p << endl;
    p++;
}
```

### Iterating with Iterator

The iterator is an object which points to a certain element in the vector. It is essentially the same as declaring pointer variable. However, the iterator is better in terms of readability.

``` cpp
for(vector<int>::iterator it = vec.begin(); it != vec.end(); ++it) {
    cout << *it << endl;
}
```

## Inserting Elements

### At End

```cpp
vec.push_back(val);
```

### At Index

To insert an element at a certain index, create an iterator, then point it to the index you want to insert the element at. After that, you use the `insert` function to insert the new element at the iterator's position.

Doing this does not replace the element at the index, but just shifts all the other elements to the right and inserts the new element at the index.

```c++
auto it = vec.begin();
```

To point the iterator to the index you want, you can use the `advance` function.

```cpp
//vec = {1,2,3,4,5}
//Makes iterator point to 3rd position
advance(it, 2);
//Inserts 5 at 3rd position
vec.insert(it, 5); //vec = {1,2,5,3,4,5}
```

Another method is using the `+` operator, and the index at which it will point is equal to the number inputted

```cpp
//vec = {1,2,3,4,5}
//Inserts 5 at index 2/the 3rd position
vec.insert(it + 2, 5) //vec = {1,2,5,3,4,5}
```

### Multiple Elements at Index

The `insert` function with 3 parameters will insert n occurrences of an elements starting from where the iterator is pointed

```cpp
//vec = {1,2,3,4,5}
//Inserts 2 occurences of '7' at 4th position
vec.insert(vec.begin() + 3,2,7); //vec = {1,2,3,7,7,4,5} 
```

### Assign Multiple Elements 

The `assign` method assigns `n`occurences of an element to the vector. This method will overwrite the vector5

```cpp
//Vector has 2 occurences of '3'
vec.assign(3,2);
```

You can also use the `assign` method to assign the vector the value from a certain range of a vector

```cpp
//v = {1,2,3,4,5}
vec.assign(v.begin() + 2, v.end()); //vec = {3,4,5}
```

## Changing Elements

### By Reference

You can reference to an element in the vector using the `[]` and then use the `=` operator to change the value of that element

```cpp
//vec = {1,2,3,4,5}
vec[2] = 6; //vec = {1,2,6,4,5}
```

### By Swapping

You can change all the elements in a vector by swiping with another

```cpp
//vec1 = {1,2,3,4,5}
//vec2 = {5,4,3,2,1}
vec1.swap(vec2); //vec1 = {5,4,3,2,1}, vec2 = {1,2,3,4,5}
```

## Removing Elements

### At End

```cpp
vec.pop_back();
```

### At Index

```cpp
auto it = vec.begin();
//Removes 3rd element
vec.erase(it + 2);
```

### Erase Function

The `erase` function takes an iterator, erases the element its pointed to, and then returns an iterator pointing to the element after it

```cpp
//vec = {1,3,6,9}
auto it = vec.erase(vec.begin() + 1); //vec = {1,6,9}
cout << *it; //6
```

### Certain Range

Create two iterators, one pointing to the first element, and another pointing to the last element

```cpp
auto itFirst = vec.begin();
auto itLast = itFirst + 3;
lst.erase(itFirst, itLast);
```

### All Elements

```cpp
vec.clear();
```

## Capacity Methods

### Checking Size

The `size()` function returns the number of elements in the vector

### Checking the Max Size

The `max_size()` function returns the max number of elements that the vector can hold

### Check the Capacity

The `capacity()`function returns the size of storage spaces allocated to the vector

```cpp
//vec = {1,2,3,4,5}
vec.size(); //5
vec.capacity(); //8
```

 ### Check if Empty

The `empty()` returns a `boolean` based on if the vector is empty or not





