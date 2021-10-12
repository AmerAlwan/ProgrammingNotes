# QuickSort

## Details

Quick sort is a divide and conquer and in-place algorithm that acts recursively and barely uses storage.

The worst case of quicksort is O(n^2) while the average case is O(nlog_2n)

Quick sort selects a value called the `pivot value`, which functions at assisting with the splitting of the list. The pivot can be:

- The first element
- The last element
- A random element
- The median

Having a good pivot element ensures that the sorting algorithm will function effectively. 

### Divide

The first step is dividing. After the pivot is chosen, rearrange the array so that all elements that are smaller than the pivot are moved to the left and all elements greater are moved to the right. This procedure is called `Partitioning`. 

### Conquer

Conquer by recursively sorting the subarrays  which are less than or equal to the pivot `array[p..q-1]`, and all subarrays which are greater than the pivot `arraypq+1..r`.

### Combine

Combine by doing nothing. Once the conquer step recursively sorts, it is done.

### Example

Given `arr = [6,3,11,4,9,8,17,7]`

1. `pivot = 6, arr = [4,3,11,6,9,8,17,7], low = 0, high = 7, i = 1, j = 2`
2. `pivot = 4, arr = [3,4,11], i = 1, j = 0, low = 0, high = 2`
3. `pivot = 4, arr = [4, 11], i = 2, j = -1, low = 1, high = 2`
4. Go back to 1 -> `pivot = 6, arr = [3,4,11,6,9,8,17,7], i = 1, j = 2, low = 0, high = 7`
5. `pivot = 4, arr = [4,11,6,9,8,17,7], i = 2, j = 1, low = 1, high = 7`
6. `pivot = 11, arr = [7,6,9,8,17,11], i = 3, j = 6, low = 2, high = 7`
7.  `pivot = 7, arr = [6,7,9,8,17], i = 3, j = 2, low = 2, high = 6`

## Java Implementation

```java
public void quicksort(int[] nums, int low, int high) {
    int i = low, j = high;
    int pivot = nums[low];
    while(i <= j) {
        while(nums[i] < pivot) {
            i++;
        }
        while(nums[j] > pivot) {
            j--;
        }
        
        if(i <= j) {
            exchange(nums, i, j);
            i++;
            j--;
        }
    }
    
    if(low < j) {
		quicksort(nums, low, j);
    }
    if(i < high) {
        quicksort(nums, i, high);
    }
}

private void exchange(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```

