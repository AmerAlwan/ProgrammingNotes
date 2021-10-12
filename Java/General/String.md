# String

## String Buffer

String is thread safe

## String Builder

StringBuilder is mutable, menaing that you can change it without making a new string copy

### Set Char At

```java
sb.setCharAt(0, 'T');
```

### Reverse

Since StringBuilder is mutable, you can use the `reverse()` function

### Add New String

```java
sb.append("new");
```

### Replace

In StringBuilder, the `replace` function acts as a `replaceAll`. The difference is that in `replaceAll()`, you can use regular expressions