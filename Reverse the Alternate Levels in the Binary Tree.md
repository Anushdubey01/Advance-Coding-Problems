
## Problem Statement

**Title**: Reverse the Alternate Levels in a Binary Tree

### Problem Description:
Write a program to reverse the alternate levels in a binary tree.

### Constraints:
- The binary tree should have only unique values.

### Input Format:
1. The first input consists of an integer `n`, representing the number of tree elements.
2. The second input consists of the root element.
3. The third input consists of `n-1` elements separated by spaces, which represent the values of the rest of the nodes in the binary tree.

### Output Format:
The output consists of the modified binary tree, where the alternate levels are reversed.

---

### Sample Test Case 1:
**Input:**
```
8
5
2 4 8 6 7 3 9
```

**Output:**
```
8 7 4 5 6 3 2 9
```

---

## Solution

The following Java program solves the problem of reversing alternate levels in a binary tree.

### Java Code:

```java
import java.io.*;
import java.lang.*;
import java.util.*;

class Tree {
    static class Node {
        int value;
        Node left, right;

        Node(int value) {
            this.value = value;
            left = null;
            right = null;
        }
    }

    public void preorder(Node root1, Node root2, int lvl) {
        if (root1 == null || root2 == null)
            return;

        int t;
        if (lvl % 2 == 0) {
            t = root1.value;
            root1.value = root2.value;
            root2.value = t;
        }

        preorder(root1.left, root2.right, lvl + 1);
        preorder(root1.right, root2.left, lvl + 1);
    }

    public void reverseAlternate(Node root) {
        preorder(root.left, root.right, 0);
    }

    public void printInorder(Node node) {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        System.out.print(node.value + " ");
        printInorder(node.right);
    }

    public void insert(Node node, int value) {
        if (value < node.value) {
            if (node.left != null) {
                insert(node.left, value);
            } else {
                node.left = new Node(value);
            }
        } else if (value > node.value) {
            if (node.right != null) {
                insert(node.right, value);
            } else {
                node.right = new Node(value);
            }
        }
    }

    public static void main(String args[]) {
        int i;
        Tree tree = new Tree();
        Scanner sc = new Scanner(System.in);
        int n = Integer.parseInt(sc.nextLine());
        Node root = new Node(Integer.parseInt(sc.next()));

        for (i = 0; i < n - 1; i++) {
            int ele = Integer.parseInt(sc.next());
            tree.insert(root, ele);
        }

        tree.reverseAlternate(root);
        tree.printInorder(root);
    }
}
```

---

### Explanation:

1. **Tree Structure**:
    - A class `Node` is defined to represent each node in the binary tree, containing `value`, `left`, and `right` pointers.
  
2. **Preorder Traversal**:
    - The method `preorder(Node root1, Node root2, int lvl)` performs a preorder traversal of the binary tree, swapping values of nodes at alternate levels.

3. **Inorder Traversal**:
    - The `printInorder(Node node)` method prints the tree nodes in inorder after performing the required modifications.

4. **Insert Method**:
    - The `insert(Node node, int value)` method inserts a new node with the given `value` into the tree based on binary search tree properties.

5. **Main Method**:
    - The `main` method takes input, constructs the binary tree, applies the reversal of alternate levels, and then prints the resulting tree in inorder.

---

### Time Complexity:
- The time complexity of the solution is O(n), where `n` is the number of nodes in the binary tree. This is because we are performing a single traversal (preorder) to swap alternate levels and another traversal (inorder) to print the tree.
