# List 

## Boxing

### Creating Boxed Variable

```java
Integer i = 1;
```

### Creating Boxed List

```java
List<Integer> l1 = new ArrayList<>(Arrays.asList(1,2,3,4));
//Mutable
List<Integer> l2 = new ArrayList<>(List.of(1,2,3,4)); 
//Immutable -> Cannot add or remove variables
List<Integer> l3 = List.of(1,2,3,4); 
```

### Converting to Boxed List

```java
//arr = {1,2,3,4}
List<Integer> l4 = Arrays.asList(Arrays.stream(arr).boxed().toArray(Integer[]::new));
```

```java
List<Integer> l5 = Arrays.stream(arr).boxed().collect(Collectors.toList())
```

## Unboxing

### Creating Unboxed Variable

```java
int i2 = i;
```

### Convert to Unboxed Array

```java
int[] arr = lst.stream().mapToInt(i->1).toArray();
```

