# Stair Search

## Details

Used to find a target in an `m x n` matrix with sorted rows and sorted columns but where the numbers in each row do not follow the numbers of the previous row. This means that this problem cannot be solved by treating the matrix as one array.

```
[ //--> Decreasing
  [1,   4,  7, 11, 15], //  |
  [2,   5,  8, 12, 19], //  |
  [3,   6,  9, 16, 22], // \_/
  [10, 13, 14, 17, 24], // Increasing
  [18, 21, 23, 26, 30]
]
```

To solve this problem, you have to start at a corner where the numbers either increase vertically and decrease horizontally, or decrease vertically and increase horizontally. 

These two corners are the **bottom-left** and **top-right** corners. You can choose either of them.

1. Say you choose the **top-right** corner, compare the number there to the target number.

2.  If the target number is bigger, then move on to the element below the corner number. If the target is smaller, then move to the element to the left. 

3. Compare the target number to that new element. 

4. Repeat these steps until you reach the target.

5. The **bottom-left** corner is the same, except with a bigger number, you move right, while with a smaller number, you move up.

   23, 26, 30]

## Implementation

### Java (Top-Right)

```java
public boolean stairSearch(int[][] matrix, int target) {
    int row = 0, col = matrix[0].length;
    while(row < matrix.length && col >= 0) {
        if(matrix[row][col] == target) {
            return true;
        }
        if(target > matrix[row][col]) {
            row++;
        } else if(target < matrix[row][col]) {
            col--;
        } else {
            return false;
        }
    }
    return false;
}
```

