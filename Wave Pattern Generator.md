## Problem Overview

This program generates a wave-like pattern based on an integer input `N`. The wave pattern consists of vertical bars ("|") printed in a specific arrangement. The pattern simulates a series of waves where each wave consists of multiple vertical bars placed with spaces between them. The height and structure of the wave pattern depends on the value of `N`.

## Problem Statement

### Task:
Write a program to create a wave-like pattern using vertical bars (`|`) with the following properties:

- The input consists of a single integer `N` (the height of the wave).
- The output displays the wave pattern of height `N` where each wave is represented by bars (`|`) arranged in a specific pattern with appropriate spacing.

### Input Format:
- A single integer `N` (height of the wave).

### Output Format:
- The output displays the wave-like pattern based on the value of `N`.

---

## Sample Test Cases

### Input 1:
```
7
```

### Output 1:
```
      |           |           |           |      
     | |         | |         | |         | |     
    |   |       |   |       |   |       |   |    
   |     |     |     |     |     |     |     |   
  |       |   |       |   |       |   |       |  
 |         | |         | |         | |         | 
|           |           |           |           |
```

### Input 2:
```
5
```

### Output 2:
```
    |       |       |       |    
   | |     | |     | |     | |   
  |   |   |   |   |   |   |   |  
 |     | |     | |     | |     | 
|       |       |       |       |
```

---

## Solution

### Java Code:

```java
import java.util.*;

class Main {
    public static void main(String args[]) {
        int wL = 4; // Width multiplier (for spacing between bars)
        Scanner sc = new Scanner(System.in);
        int waveHeight = sc.nextInt(); // Read the height of the wave
        int wH = waveHeight - 1;
        int x = wH;

        // Loop through each row
        for (int i = 0; i <= wH; i++) {
            // Loop through each column (based on calculated width)
            for (int j = 0; j <= wH * wL * 2; j++) {
                // Check if the current position should print a vertical bar
                if (j % (wH * 2) == x || j % (wH * 2) == wH + i) {
                    System.out.print("|");
                } else {
                    System.out.print(" ");
                }
            }
            x--; // Decrease the spacing for the next row
            System.out.println(); // Move to the next row
        }
    }
}
```

---

## Time and Space Complexity Analysis

### Time Complexity:
- The program iterates through `wH + 1` rows (where `wH = N - 1`), and for each row, it iterates through `wH * wL * 2` columns.
- In each iteration of the inner loop, it checks conditions and prints characters. Therefore, the total time complexity is proportional to `O(N^2)`, where `N` is the input height of the wave.
  
  **Overall Time Complexity: O(N^2)**

### Space Complexity:
- The space used by the program is constant, as it does not store any large data structures.
- The only memory used is for the input and a few integer variables. Therefore, the space complexity is `O(1)`.

  **Overall Space Complexity: O(1)**

---

## Conclusion

This program efficiently generates a wave pattern based on the height specified by the user. It uses simple loops to position vertical bars and spaces to create the desired visual effect. The time complexity is quadratic due to the nested loops iterating through rows and columns. The space complexity is constant, making the program memory efficient.
