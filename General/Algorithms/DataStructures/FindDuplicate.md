# Find Duplicate

## Data Structure with any range elements

### Brute Force

The brute force solution uses two nested for loops and takes O(n^2)  time complexity with O(1) space complexity.

#### Java Implementation

```java
public int findDup(int[] arr) {
    for(int i = 0; i < arr.length; i++) {
        for(int j = i + 1; j < arr.length; j++) {
            if(arr[i] == arr[j]) {
                return arr[i];
            }
        }
    }
}
```

### Count Iterations

This solution uses a HashMap to count the number of iterations of each element. The time complexity of this solution is O(n) and the space complexity is O(n).

#### Java Implementation

```java
public int findDup(int[] arr) {
    HashMap<Integer, Integer> hm = new HashMap<>();
    for(int i : arr) {
        if(hm.contains(i)) {
            hm.put(i, hm.get(i) + 1);
        } else {
            hm.put(i, 1);
        }
    }
    
    for(Map.Entry e : hm.entrySet()) {
        if(e.getValue() > 1) {
            return e.getKey();
        }
    }
}
```

### Sort Array (Alters Original Data)

By sorting the array, any two duplicates will be right next to each other, making checking for them just as easy. This solution does however alter the array by sorting it. The time complexity of this is solution is O(nlog(n)) but it may depend on the sorting algorithm used, and space complexity is O(1).

#### Java Implementation

```java
public int findDup(int[] arr) {
    Arrays.sort(arr);
    for(int i = 0; i < arr.length - 1; i++) {
        if(arr[i] == arr[i+1]) {
            return arr[i];
        }
    }
}
```

## Data Structure with Elements in Range of 1...n

### Count Iterations

This solution uses an array to count the number of iterations of each element. Each element in the original array represents an index in the counting array. The time complexity of this solution is O(n) and the space complexity is O(n).

#### Java Implementation

```java
public int findDup(int[] arr) {
    //arr.length - 1 cause one of the elements is a duplicate
	int[] count = new int[arr.length - 1];
    //The elements go from 1...n, but the array goes from 0...n-1
    for(int i : arr) {
        count[i-1]++;
        if(count[i-1] > 1) {
            return i;
        }
    }
}
```

### Sum of the Elements

First, get the sum of the elements from 1 + 2 + ... n, and then get the sum of the elements in the array. Subtract them and you will get the extra element. The time complexity of this solution is O(n) and the space complexity is O(1).

**Note:** This solution does not work if there are multiple duplicates.
**Ex: ** 1, 2, 2, 3, 3, 4

#### Java Implementation

```java
public int findDup(int[] arr) {
    int completeSum = 0;
    for(int i = 1; i <= arr.length - 1; i++) {
        completeSum += i;
    }
    int sum = 0;
    for(int i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    
    return sum - completeSum;
    
}
```

### Marker (Alters Original Data Structure)

Since each of the elements range from 1...n, each value in the array has its own corresponding index in the array. 

This solution considers the array as a sort of linked list where any index is pointing to the value of that index. We would iterate over each element and mark its corresponding index by setting its sign to negative. Then when we check the value of that element again, if it is negative, it means it is a duplicate.

This solution runs in O(n) time and O(1) space

#### Java Implementation

```java
public int findDup(int[] arr) {
    for(int i = 0; i < arr.length; i++) {
        if(arr[Math.abs(arr[i])] > 0) {
            arr[Math.abs(arr[i])] *= -1;
        } else {
            return Math.abs(arr[i]);
        }
    }
}
```

### Runner  with Floyd's cycle-finding Algorithm (Does Not Alter Original Data Structure)

Just like the marker solution, this technique also treats the data structure as if it was a linked list. We simply say that a duplicate exists because a cycle within the linked list exists.

This solution also has a O(n) time complexity and O(1) space complexity

The steps are:

1. Initiate two pointers, slow and fast
2. For each step, slow is moving one step at a time
3. For each step, fast is moving two steps at a time
4. When slow == fast, we are in a cycle
5. After the cycle is discovered, reset slow and move both pointers step by step until they are equals again

#### Java Implementation

``` java
public int findDup(int[] arr) {
    int slow = arr[0];
    int fast = arr[arr[0]];
    while(fast != slow) {
        slow = arr[slow];
        fast = fast[arr[fast]];
    }
    slow = 0;
    while(fast != slow) {
        slow = arr[slow];
        fast = arr[fast];
    }
    return slow;
}
```





