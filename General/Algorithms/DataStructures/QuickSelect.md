# Quick Select

Quick select is an algorithm used to find the k-th biggest/smallest element in an array. Quick Select is similar to **Quick Sort**, except you realize that you do not actually need to completely quick sort the array, we only need to rearrange its contents so that the *k-th* element of the array is the *k-th* largest or smallest.

In `QuickSort`, we pick a pivot element and move it so its correct position. We also partition the array around it.

In `QuickSelect`, the idea is to stop at the point where the pivot itself is the *k-th* largest element.

**Optimization: **The algorithm can be further optimized if we don't recur for both left and right sides of the pivot. We only need to recur for one of them according to the position of the pivot.

## Details

* Pick a pivot element and partition the array accordingly
  * Pick the rightmost element as pivot
  * Reshuffle the array such that pivot element is placed at its rightful place - all elements less than the pivot would be at lower indexes, and elements greater than the pivot would be placed at higher indexes than the pivot
* If pivot is placed at the *k-th* element in the array, exit the process, as pivot is the *k-th* largest element
* If pivot position is greater than k, then continue the process with the left subarray, otherwise, recur the process with right subarray.

**Biggest vs Smallest: ** If we sort the array in ascending order, the *k-th* element of an array will be the *k-th* smallest element. To find the *k-th* largest element, we can pass `k = arr.length - k`

## Implementation

### Java Implementation

```java
public int quickSelect(int[] arr, int left, int right, int k) {
    if(k >= 0 && k <= right - left + 1) {
        int pos = parition(arr, left, right);
        if(pos - left == k) {
            return arr[pos];
        }
        if(pos - left > k) {
            return quickSelect(arr, left, pos - 1, k);
        }
        return quickSelect(arr, pos + 1, right, k - pos + left - 1)''
    }
    return 0;
}

public int partition(int[] arr, int left, int right) {
    int pivot = arr[right], i = left;
    for(int j = left; j <= right - 1; j++) {
        if(arr[j] <= pivot) {
            swap(arr, i, j);
            i++;
        }
    }
}

public void swap(int[] arr, int n1, int n2) {
	int temp = arr[n2];
    arr[n2] = arr[n1];
    arr[n1] = temp;
}
```



