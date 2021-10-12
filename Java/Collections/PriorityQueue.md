# Priority Queue

## Creating Queue

In Java, a priority queue by default sorts in a min queue.

### Without Comparator

```java
//Creates min queue
PriorityQueue<Integer> pq = new PriorityQueue<>();
```

### With Comparator

```java
//Creates max queue
PriorityQueue<Integer> pq = new PriorityQueue<>((a,b) -> b-a);
```

## Examples

### Sort Students by Grade and list by name

In this problem, you are given a list of  students. Get the top student and list them by name.

```java
PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> b[1] - a[1]);
pq.add(new int[] {20109, 99});
pq.add(new int[] {28110, 98});
pq.add(new int[] {20111, 85});
System.out.println(pq.remove()[0]); //20109
```

