# Iterator

An `Iterator` is a design patron and its useful for common problems, which in this case, is used to iterate through most collections

## Creating Iterator

When you create an iterator, it does not point anywhere (It is kind of pointing between elements). So, to get the first element is calling the `next()` method.

```java
//Collection<String> c;
Iterator<String> itr = c.iterator()
```

## Iterating 

In java, you must check if there is an element next by using the `hasNext()` function, then calling the `next()` function which will return the element.

Once `next()` has been called, the iterator cannot be backtracked. So to go to a previous element, you need a whole new iterator.

```java
//Collection<String> c;
while(itr.hasNext()) {
    String element = itr.next();
}
```

## Implicant Use

## Examples

### Iterating through String Characters

#### Implicitly

```java
//s = "programming class"
//Forward
for(char c : s.toCharArray()) {
    //
}
//Reverse
List<Character> lst = Arrays.stream(s.toCharArray()).boxed().collect(Collectors.tolist());
Collections.reverse(lst);
Character[] c = lst.stream().unboxed().
for()
```



