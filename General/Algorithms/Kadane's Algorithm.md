# Kadane's Algorithm

## Details

Kadane's algorithm is a dynamic programming algorithm used to calculate some sum while considering every subarray within an array with a runtime of O(n).

### Steps to calculate maximum sum subarray

In a typical brute force approach, you would look at each index and consider what the maximum subarray ending at that index is. Ex: At index **0**, it is `[1]`. At index **1**, it is `[-3]` and `[1, -3]`. At index **2**, it is`[2]`, `[-3, 2]`, and `[1, -3, 2]`.

In kadane's algorithm, at any index, the local maximum subarray is either the current element or the current element combined with the previous maximum subarray

1. Start with the first element being `max_sum`. Have another variable called `current_sum` which is also set to the first element.
2. At each index, take the element and see if it is bigger than itself added to the `current_sum`. So, is `arr[x] > arr[x] + current_sum`. If it is, then we set `current_sum` equal to it, essentially starting a new subarray. If not, then we just update the subarray with the element added, essentially continuing the previous subarray.
3. Compare `current_sum` to `max_sum`. If `current_sum` is bigger, then update `max_sum` to that.

### Example

Assume you have array `[1, -3, 2, 1, -1]`

1. `[1]` => `current_sum` = 1, `max_sum` = 1
2. `[1,-3]` > `[-3]` | -2 < 1 | `current_sum` = -2, `max_sum` = 1
3. `[2]` > `[1,-3,2]` | 2 > 1 | `current_sum` = 2, `max_sum` = 2
4. `[2,1]` > `[1]` |  3 > 2 | `current_sum` = 3, `max_sum` = 3
5. `[2,1,-1]` > `[-1]` | 3 > 2 | `current_sum` = 2, `max_sum` = 3
6. *Return 3*, which is the subarray `[2,1]`

## Implementation

### Java implementation of max sum subarray

```java
public int maxSumSubarray(int[] arr) {
    int current_sum = arr[0], max_sum = arr[0];
    for(int i = 1; i < arr.length; i++) {
        current_sum = Math.max(arr[i], current_sum + arr[i]);
        max_sum = Math.max(current_sum, max_sum);
    }
    return max_sum;
}
```





