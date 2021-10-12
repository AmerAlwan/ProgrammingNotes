# Streaming

## Parallel

Parallel is used in distributive computing where you have multiple computers or processers and you want to distribute the data to all processors so the data can be distributed in parallel, making the process faster.

### Stream

When making a stream, use the `parallelStream()` function instead of `stream()`. This makes multiple streams that work simultaneously without interrupting or having to lock each other.

### Map

When making a map, use `Collectors.toConcurrentMap()`, as using `Collectors.toMap()` will take away from the parallelism. It makes sure that the elements with the same hashcode will go to the same processor. This is done so if you are for example counting how many words are in a sentence, you want all the same words/keys to go to the same processor, as multiple processors wouldn't know that they have the same key and therefore the word count would be wrong.

