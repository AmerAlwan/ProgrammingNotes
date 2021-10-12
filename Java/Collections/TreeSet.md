# TreeSet

With tree, the worst-case time complexity is O(log(n)). Meanwhile, depending on the hashing algorithm, the worst-case time complexity could reach O(n).

### Creating TreeSet from List

```java
//l1 = {1,2,4,5};
TreeSet<Integer> ts = new TreeSet<>(l1);
```

## Range

A useful feature with `TreeSet` that allows you to check if a certain range of numbers is inside the `TreeSet`

### Floor

Given input `var`, it checks if the `TreeSet` contains `var` or any variable with a value equal to or lower than `var` (Kind of like lower than or equal to)

```java
ts.floor(5) //5
```

### Lower

Given input `var`, it checks if the `TreeSet` contains any variable with a value lower than `var` (Kind of like lower than)

```java
ts.lower(5) //4
```

### Ceiling

Given input `var`, it checks if the TreeSet contains any variable with a value equal to or higher than `var`

```java
ts.ceiling(2); //2
```

### Higher

Given input `var`, it checks if the TreeSet contains any variable with a value higher than `var`

```java
ts.higher(2); //4
```

## Iterating Through TreeSet

### Using for loop

```java
for(int i : ts) {
    //
}
```

