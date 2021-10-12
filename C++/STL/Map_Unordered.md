# Map

Maps are containers that store elements in a key and value fashion

## Creating a Map

```cpp
map<int, int> mp { {1,10}, {2,20} };
```

## Iterating through Map

```cpp
for(map<int, int>::iterator it = mp.begin(); it != mp.end(); ++it) { 
    cout << it->first << " " << it->second << endl;
	 endl;
}
```

```cpp
for(auto it = mp.begin(); it != mp.end(); ++it) { 
    cout << (*it).first << " " << (*it).second << endl;
}
```

```cpp
for(auto it : mp) {
    cout << it.first << " " << it.second << endl;
}
```

## Inserting Elements

### Inserting New Element

The `insert` function is used to insert elements into a map. 

```cpp
//Inserts element with the key '1' and the value '10'
mp.insert({ 1, 10 });
```

Alternatively, you can use `pair<T, T2>` as the parameter

```cpp
mp.insert(pair<int, int> (1,10));
```

### Insert Elements from other Map

You can use the `insert` function to also insert elements in a certain range of another map

```cpp
mp2.insert(mp.begin(), mp.end());
```

## Getting Elements

### Getting Element by Key using Pointer

Use the `find(key)` function to get an `iterator` pointing to the element with the inputted key

### Getting Element by Key Using Reference

Use the `at(key)` function which returns a reference to the element, but does not insert any element not in the map

```cpp
//mp = {1,10}
cout << mp.at(1); //10
```

You can also use the `[]` operator, which will return a reference but also insert any element not in the map

```cpp
//mp = {1,10}
cout << mp[1]; //10
```

### Getting Element by Value

C++ has no specified function that does this, so you have to make your own

```cpp
for(auto it = mp.begin(); it != mp.end(); ++it) 
    if(it->second == value) 
        return it->first;
```

### Getting Element by Bound

Using either `upper_bound` or `lower_bound`, you can get the `iterator` pointed to the element with the next key that is higher or lower than your inputted key

```cpp
//mp = {1,10}, {5, 50}, {10, 100}
it = mp.upper_bound(5); //{10,100}
it = mp.lower_bound(5); //{1,10}
//When the inputted key is higher than the highest key or lower than the lowest key, then the key is returned as the size of the map and the value is returned as 0
it = mp.upper_bound(20); //{3, 0}
```

## Changing Elements

### Changing Value using Pointer

To change the value of an element, you need to use an `iterator` that is pointed to that element using the `find(key)` function. Then, use the `->` to point to the value, and then use the `=` operator to set the current value to a new value

```cpp
//mp = {1,40}, {2, 50}
auto it = mp.find(1);
if (it != mp.end()) 
    it->second = 42;
//mp = {1,42}, {2,50}
```

### Changing Value using Reference

You can use the `[]` operator to <u>create</u> or <u>change</u> the value of an element using the format `mp[key] = value`

```cpp
//mp = {1,10}
mp[2] = 20;
//mp = {1,10}, {2,20}
mp[1] = 20; //mp = {1,10}, {2,20};
```

### Changing Elements Using Swapping

Use the `swap` method to swap the elements of two maps

```cpp
//mp1 = {1,10}, {2,20}
//mp2 = {3,30}, {4,40}
mp1.swap(mp2); //mp1 = {3,30}, {4,40} //mp2 = {1,10}, {2,20}
```

## Removing Elements

### Removing Element with Key

The `erase(key)` function will remove the element with the inputted key. If the key element is found, then the function returns `1`, else it returns `0`

```cpp
//mp = {1,10}, {2,20}
int num = mp.erase(1); //1 //mp = {2,20} 
```

### Removing Element with Iterator

```cpp
//mp = {1,10}, {2,20}
auto it = mp.find(1);
mp.erase(it); //1 //mp = {2,20}
```

### Removing Elements with Bound

```cpp
//mp = {1,10}, {2,20}, {3,30}, {4,40}
mp.erase(mp.find(1), mp.find(2)); //1 //mp = {3,30}, {4,40}
```

### Removing All Elements

Use the `clear()` function to remove all elements from the map

## Examples

### Display  Number of Time  each Value in Vector is Repeated

```cpp
vector<int> v = {1,2,3,1,3,2,1,1,2,1};
map<int, int> counter;
//With the [] operator, if a key is not existant, it will create a new element with that key and a value of '0'
for(int n : v) counter[n]++;
for(auto it : counter) cout << it.first << ": " << it.second << ", ";
```

`Output: 1: 4, 2: 3, 3:2`

# Multi map

# Unordered Map

# Unordered Multi Map


