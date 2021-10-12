# Find Duplicate and Missing Elements

```java
List<Integer> lst = new ArrayList<>(2);
```

## Sorting

You can first sort the array and then find the duplicate and missing elements. This does however alter the original array. 

The time complexity is `O(nlogn)` and space complexity is `O(logn)`

### Java Implementation

```java
public List<Integer> findErr(int[] nums) {
    Arrays.sort(arr);
    int dup = -1, missing = -1;
    for(int i = 1; i < nums.length; i++) {
        if(nums[i] == nums[i-1]) {
            dup = nums[i];
        } else if(nums[i] > nums[i-1] + 1) {
            missing = nums[i-1] + 1;
        }
        lst.add(dup);
        lst.add(missing);
        return lst;
    }
}
```

## Count Array

Similar to the count technique to find duplicate element, this technique works the same where the duplicate element would have a > 1 count and the missing element would have a count of 0.

This solution has a time complexity of O(n) and space complexity of O(n)

```java
public List<Integer> findErr(int[] nums) {
    int dup = -1, missing = -1;
    int[] count = new int[nums.length];
    for(int i = 0; i < nums.length; i++) {
        count[nums[i]-1]++;
        if(count[nums[i]-1] > 1) {
            dup = nums[i];
        }
    }
    
    for(int i = 0; i < count.length; i++) {
        if(count[i] == 0) {
            missing = i + 1;
        }
    }
    lst.add(dup);
    lst.add(missing);
    return lst;
}
```

## Mark Visited Indexes as Negative

This solution alters the original data set, but has O(n) time complexity and O(1) space complexity

```java
public List<Integer> findErr(int[] nums) {
    int dup = -1, missing = -1;
    for(int i = 0; i < nums.length; i++) {
        int index = Math.abs(nums[i]) - 1;
        if(nums[index] > 0) {
            nums[index] *= -1;
        } else {
            dup = nums[index];
        }
    }
    for(int i = 0; i < nums.length; i++) {
        if(nums[i] > 0) {
            missing = i+1;
        }
    }
    lst.add(dup);
    lst.add(missing);
    return lst;
}
```

