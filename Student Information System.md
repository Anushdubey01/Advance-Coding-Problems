## Problem Overview

In this problem, we need to implement a **Student** class with attributes like roll number, name, age, and course. The class should accept values for these attributes through a parameterized constructor and raise custom exceptions for invalid values.

The two exceptions we need to handle are:
1. **AgeNotWithInRangeException**: Raised when the age of the student is not between 15 and 21 (inclusive).
2. **NameNotValidException**: Raised when the student's name contains any digits or special characters.

The goal is to ensure that the student details are validated and displayed appropriately, with exception messages when the validation fails.

---

## Problem Statement

### Task
Create a class `Student` with attributes:
- `roll` (integer)
- `name` (string)
- `age` (integer)
- `course` (string)

### Requirements
1. The constructor should accept values for roll number, name, age, and course.
2. If the student's age is not between 15 and 21 (inclusive), an exception **AgeNotWithInRangeException** should be thrown.
3. If the student's name contains numbers or special symbols, an exception **NameNotValidException** should be thrown.
4. Handle these exceptions and print appropriate messages with the student details.
5. The program should display the student's details if both name and age are valid.

### Input Format:
- The first line of input consists of an integer representing the student's roll number.
- The second line consists of a string representing the student's name.
- The third line consists of an integer representing the student's age.
- The fourth line consists of a string representing the student's course.

### Output Format:
- If both the name and age are valid, print the student's details.
- If the age is not valid, print: 
    - `"Age is not between 15 and 21"` followed by the student's details.
- If the name is not valid, print:
    - `"Name is not Valid"` followed by the student's details.

---

## Sample Input & Output

**Input 1:**

```
100
Babu
21
MCA
```

**Output 1:**

```
100 Babu 21 MCA
```

**Input 2:**

```
100
Babu
24
MCA
```

**Output 2:**

```
Age is not between 15 and 21
100 Babu 24 MCA
```

**Input 3:**

```
100
Babu3
20
MCA
```

**Output 3:**

```
Name is not Valid
100 Babu3 20 MCA
```

---

## Solution

```java
import java.util.Scanner;

class AgeNotWithInRangeException extends Exception {
    public String toString() {
        return ("Age is not between 15 and 21");
    }
}

class NameNotValidException extends Exception {
    public String toString() {
        return ("Name is not Valid");
    }
}

class Student {
    int roll, age;
    String name, course;

    // Default constructor
    Student() {
        roll = 0;
        name = null;
        age = 0;
        course = null;
    }

    // Parameterized constructor
    Student(int r, String n, int a, String c) {
        roll = r;
        course = c;
        int l, temp = 0;
        l = n.length();
        
        // Check if name contains invalid characters (numbers or symbols)
        for (int i = 0; i < l; i++) {
            char ch = n.charAt(i);
            if ((ch < 'A' || ch > 'Z') && (ch < 'a' || ch > 'z')) {
                temp = 1;
            }
        }
        
        try {
            if (temp == 1) {
                name = n;
                throw new NameNotValidException();
            } else {
                name = n;
            }
        } catch (NameNotValidException e2) {
            System.out.println(e2);
        }

        try {
            if (a >= 15 && a <= 21) {
                age = a;
            } else {
                age = a;
                throw new AgeNotWithInRangeException();
            }
        } catch (AgeNotWithInRangeException e1) {
            System.out.println(e1);
        }
    }

    // Method to display student details
    void display() {
        System.out.println(roll + " " + name + " " + age + " " + course);
    }
}

class StudentDemo {
    public static void main(String args[]) {
        Scanner br = new Scanner(System.in);
        int roll = Integer.parseInt(br.nextLine());
        String name = br.nextLine();
        int age = Integer.parseInt(br.nextLine());
        String course = br.nextLine();
        
        // Create a student object and display the details
        Student s = new Student(roll, name, age, course);
        s.display();
    }
}
```

---

## Time and Space Complexity Analysis

### Time Complexity:
- **Name Validation**: The name is validated by checking each character to ensure it is a letter. This takes O(n) time, where `n` is the length of the name (maximum 100 characters).
- **Age Validation**: The age validation involves a simple comparison which is O(1) in time.
- **Overall**: The overall time complexity is O(n), where `n` is the length of the student's name (since it dominates the age validation step).

### Space Complexity:
- **Student Object**: The space required for storing the student details (name, age, roll number, and course) is O(1), as these are constant-sized attributes.
- **Exception Objects**: The space used for exception objects is negligible.
- **Overall**: The overall space complexity is O(1).

---

## Conclusion

This program allows validation of student details using custom exceptions for name and age validation. The code is structured to handle user-defined exceptions and display appropriate messages for invalid data. It's a great example of how to use exception handling in object-oriented programming.
