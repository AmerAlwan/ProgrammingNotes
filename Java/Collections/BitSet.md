# BitSet

### boolean vs Boolean vs BitSet

A `boolean` is 1 byte while `Boolean` is around 4 bytes. A `BitSet` is created effeciently as youre making an array made up of bits, and so it is a huge memory saver and it has operations to go with it.

## Creating BitSet

```java
BitSet bs = new BitSet(10);
```

## Setting Values

### Set to true

To set a bit to true, you use the `set()` method which will set the bit value to 1, whih is equal to true.

```java
//Sets the indexes from 8 to 9 to value 1
bs.set(8,9);
```

## Operations

### OR

### XOR

### Find First Set Bit

```java

```

### Get Size of Set

```java
bs.cardinality();
```

