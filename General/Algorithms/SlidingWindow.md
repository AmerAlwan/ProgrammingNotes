# Sliding Window

## Details

The sliding window problem is used with arrays/lists and that can help run through every `k` size sublist in an array in `O(n)` time. 

### Example

Assume we have an array `[1,2,3,4,5]`, a sliding window of size `3` would run over it like:

- [1,2,3]
  - [2,3,4]
    - [3,4,5]

## Implementation

### Java Implementation

This program implements the sliding window technique to find the array sub-list of size `k`with the highest sum

```java
public int maxSum(int[] arr, int k) {
    int max = 0;
    //Compute sum of first window of size k
    for(int i = 0; i < k; i++) {
        max += arr[i];
    }
        
    //Compute sums of remaining windows by removin first element of previous window and adding last element of current window
	int window = max;
	for(int i = k; i < arr.length; i++) {
        window += arr[i] - arr[i-k];
        max = Math.max(max, window);
    }
}
```





