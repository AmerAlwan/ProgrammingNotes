# HashMap

## Creating HashMap

### Without Initialization

```java
Map<String, String> m = new HashMap<>();
```

### With Initialization

```java
Map<Integer, Integer> m = new Hashmap<>(Map.of(1,1,2,2,3,3)); //1->1, 2->2, 3->3
```

## Iterating through HashMap	

### Using an Entry

`HashMap` cannot be iterated using the Collection's `Iterator` class. Instead, maps have their own iterator called an `Entry`

```java
for(Map.Entry<String, String> e : mp.entrySet()) {
    System.out.println(e.getKey() + ": " + e.getValue());
} 
```

### Using `forEach`

```java
mp.forEach((k,v) -> System.out.println(k + ": " + v));
```

## Getting Elements

### Get Elements

Use the `get` function. However, if the element does not exists, an exception is returned

### Get Element without Exception

```java
mp.getOrDefault(5,0);
```

## Putting Elements

### Put with Replace

The normal `put` function puts a value to a key. If that key already exists, it will replace its value

### Put Absent Element

```java
//mp = {1,10}, {4,40}
mp.putIfAbsent(4,0);
//mp = {1,10}, {4,40}
mp.putIfAbsent(5,0);
//mp = {1,10}, {4,40}, {5,0}
```

### Update Values

To update value (like increasing values), you can use the `merge` function

```java
mp.merge(key, defaultValue, (a,b) -> a+b);
```

## Examples

### Display Number of Times a Value is Repeated

```java
HashMap<Integer, Integer> m = new HashMap<>();
int arr[] = {1, 2, 3, 1, 2, 3, 1, 2, 4};
for(int i : arr) {
    m.merge(i, 1, (a,b) -> a+b);
}
```

