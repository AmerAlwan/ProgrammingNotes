# Maximum Product Subarray

Solving this problem uses a solution similar to Kadane's Algorithm, except that you also have to consider cases where two **negatives** multiply by each other and produce a number that is **positive**. In order to solve this problem, you will need two `current_sum` values, a max and a min one.

### Details

Since there is the possibility of there being two negative numbers, we have to use **dynamic programming** and look-ahead. 

At each iteration, we have to consider that the max product can be obtained by:

* by multiplying `nums[i]`to a previous max product
* by multiplying `nums[i]` to a previous min product (since both these numbers might be negative)
* `nums[i]` might itself be the largest

### Steps

Given `arr = [2,-5,-2,-4,3]`

1. temp = ? | current_max = 2 | current_min = 2 | max = 2 
2. temp = 2 | current_max = -5 > -10 >= -10 | current_min = -10 <= -10 < -5 | max = 2 > -5
3. temp = -5 | current_max = 20 > 10 > -2 | current_min = -2 < 10 < 20 | max = 20 > 2
4. temp = 20 | current_max = 8 > -4 > -80 | current_min = -80 < -4 < 8 | max = 20 > 8
5. temp = 8 | current_max = 24 > 3 > -240 | current_min = -240 < 3 < 24 | max = 24 > 20
6. ***return 24***

## Implementation

### Java Implementation

```java
public int maxProduct(int[] nums) {
    int current_max = nums[0];
    int current_min = nums[0];
    int max = nums[0];
    for(int i = 1; i < nums.length; i++) {
		int n = nums[i];
		int temp = current_max;
		current_max = Math.max(n, Math.max(n*current_max, n*current_min));
		current_min = Math.min(n, Math.min(n*current_min, n*temp));
		max = Math.max(max, current_max);
    }
    return max;
}
```

