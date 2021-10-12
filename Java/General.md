# General

### Getting Max /MinValue

``` java
Integer.MAX_VALUE;
Integer.MIN_VALUE;
```

### Getting Infinity

``` java
Integer.POSITIVE_INFINITY;
INTEGER.NEGATIVE_INFINITY;
```

### Writing Value in Binary

``` java
Integer i = 0b101; //13
```

## Characters

### Checking if White Space

```java
Character.isWhiteSpace('c'); //false
```

### Checking if is Letter

```java
Character.isLetter('c'); //true
```

### Checking if digit

```java
Character.isDigit('0'); //true
```

## String

### Ignore Case Sensitivity

```java
"AB".equalsIgnoreCase("ab");
```

### Check if Starts or Ends with

```java
"AB".startsWith("B", 1); //true
"AB".endsWith("B"); //true
```

## Double & Long

### Get int as Double or Long

```java
double d = 2d;
long l = 2l;
```

## Array & List

### Creating Array

```java
int[] arr = {1,2,3};
//or
int arr[] = {1,2,3};
```

### Sorting Arrays

Use the `Array.sort()` method. However, you cannot use lambda expressions for the sorting algorithm with `Arrays`, only with `Collections`.

### Convert Array to List

```java
List<Integer> lst = Arrays.stream(arr).boxed().collect(Collectors.toList());
```

### Convert List to Primative



### Reversing List

```java
Collections.reverse(lst);
```

