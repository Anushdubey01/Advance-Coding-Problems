## Problem Overview

In this task, Reenu needs to perform two main operations on strings:
1. Reverse a given string and display the reversed version.
2. Compare two strings and display whether they are the same or not, keeping in mind that the comparison is **case-sensitive**.

The program should handle:
- Reversing the first string.
- Comparing the two strings and outputting the result as either "same" or "not same".

### Input Format:
1. The first input line consists of the string `s1`.
2. The second input line consists of the string `s2`.

### Output Format:
1. The first output line displays the reversed version of string `s1`.
2. The second output line displays whether `s1` and `s2` are the same or not in the format:
   - `<s1> and <s2> are same` if both strings are identical.
   - `<s1> and <s2> are not same` if they differ.

---

## Sample Test Cases

### Input 1:
```
hello
hello
```

### Output 1:
```
olleh
hello and hello are same
```

### Input 2:
```
wonder
hello
```

### Output 2:
```
rednow
wonder and hello are not same
```

### Input 3:
```
ABC
abc
```

### Output 3:
```
CBA
ABC and abc are not same
```

---

## Solution

Here is the Java implementation for the problem:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String string1, string2, rev = "";
        int length1, length2, flag = 0;

        // Accept two input strings
        string1 = sc.next();
        string2 = sc.next();

        length1 = string1.length();
        length2 = string2.length();

        // Reverse string1 and store in rev
        for (int i = length1 - 1; i >= 0; i--) {
            rev += string1.charAt(i);
        }

        // Display reversed string
        System.out.println(rev);

        // Compare the two strings
        if (string1.equals(string2)) {
            System.out.println(string1 + " and " + string2 + " are same");
        } else {
            System.out.println(string1 + " and " + string2 + " are not same");
        }

        sc.close();
    }
}
```

---

### Explanation:
1. **String Reversal**: The string `string1` is reversed by iterating through its characters in reverse order and appending them to a new string `rev`.
2. **String Comparison**: The two strings, `string1` and `string2`, are compared using the `.equals()` method which is case-sensitive. If they are the same, the program prints that they are the same; otherwise, it states that they are not the same.
3. **Input and Output**: The program reads the two strings from the user input, reverses the first string, and compares the two strings. The results are printed accordingly.

---

## Time and Space Complexity Analysis

### Time Complexity:
- **Reversing the String**: The time complexity for reversing the string is O(n), where `n` is the length of the first string (`string1`), as each character in the string is visited once during the reversal.
- **Comparing the Strings**: The time complexity for comparing the strings is O(m), where `m` is the length of the shorter string between `string1` and `string2`. In the worst case, it can be O(n) if both strings are of equal length.
  
Thus, the overall time complexity of the program is **O(n)**, where `n` is the length of the first string.

### Space Complexity:
- **Space for String Variables**: The program uses a few string variables like `string1`, `string2`, and `rev`, which require space proportional to the length of the strings.
- **Total Space Complexity**: The space complexity is **O(n)**, where `n` is the length of the first string (`string1`), since only a few string variables and a constant number of integer variables are used.

---

## Conclusion

This program efficiently solves the problem of reversing a string and comparing two strings. It handles string operations such as reversal and comparison in a clear and concise manner. The time and space complexities are optimal given the constraints of the problem.
