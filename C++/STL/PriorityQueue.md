# Priority Queue

## Creating Queue

### Without Comparator

```cpp
priority_queue<int> pq;
```

## Adding Elements

In C++, a priority queue by default sorts elements by max priority queue

```cpp
pq.add(5);
pq.add(3);
pq.add(7);
//pq = {7, 5, 3}
```

## Examples

### Get Top Student

``` java
auto comp = [] (const pair<int, int> & a, const pair<int, int> & b) {return a.first < b.first};
//In C++, you can tell the priority queue which data structure to use. In here, you are telling it to use a vector data structure in the second parameter.
priority_queue<pair<int, int>, vector<pair<int,int>>, decltype(comp)> pq(comp);
pq.push({2,5});
pq.push({10,3});
```

