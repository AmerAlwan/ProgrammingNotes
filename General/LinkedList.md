# LinkedList

## Types

- **Single Linked List: **
- **Circular Linked List: **
- **Double Linked List: **
- **Circular Double Linked List: **
- **Header Linked List: **
- **Multi Linked List: **

## Advantages & Disadvantage

### Advantages

- An `Array` and `ArrayList` stores elements contagiously in one block in memory. Meanwhile, `LinkedList` is more dynamic, as it allocates memory for each element separately and when necessary.
- `LinkedList` is more efficient at inserting and removing elements at a specified position. Meanwhile, inserting an element in an `array` is slower because of shifting

### Disadvantages:

- Consumes more space because every node needs to store the address which points to the next node (Double Linked List are even worse since they need to store the address of the previous node)
- Memory allocation is not contagious. Therefore, searching for a particular element is time consuming
- Reverse traversing is difficult in a `forward_list`

* Non-Contiguous memory locations are not good for cache. A `LinkedList` could suffer from cache misses.

## Applications

- Implementation of graphs where each node stores adjacent vertices

- Implementation of `queue` and `stack`

- Maintaining directory of names

- Performing arithmetic operations on long integers

  