## Problem Statement

**Title**: Binary Tree Representation of a Family

### Problem Description:
In a remote village in Maharashtra, there is a belief that every family should have exactly 5 members. The rules for family structure are as follows:

1. There must be one elder family member who has exactly two children.
2. The first child must be a parent to two children, and the second child is not a parent.

A researcher connecting these rules with the binary tree concept implemented it in code. The task is to simulate this structure and explore in-order, pre-order, and post-order traversals of the binary tree.

### Input Format:
- The input consists of a single line with 5 space-separated integers representing the values of the tree members.

### Output Format:
The output displays the pre-order, in-order, and post-order traversals of the binary tree, each in a separate line.

---

### Sample Test Cases:

**Input 1:**
```
8 6 9 1 3
```

**Output 1:**
```
Preorder traversal:
8 6 1 3 9
Inorder traversal:
1 6 3 8 9
Postorder traversal:
1 3 6 9 8
```

---

**Input 2:**
```
-12 -36 -45 -78 -21
```

**Output 2:**
```
Preorder traversal:
-12 -36 -78 -21 -45
Inorder traversal:
-78 -36 -21 -12 -45
Postorder traversal:
-78 -21 -36 -45 -12
```

---

## Solution

### Python Code:

```python
class N:
    def __init__(self, v):
        self.v = v
        self.l = None
        self.r = None

def p(n):
    if n is None: return []
    return [n.v] + p(n.l) + p(n.r)

def i(n):
    if n is None: return []
    return i(n.l) + [n.v] + i(n.r)

def q(n):
    if n is None: return []
    return q(n.l) + q(n.r) + [n.v]

def b(v):
    r = N(v[0])
    l = N(v[1])
    r1 = N(v[2])
    r.l = l
    r.r = r1
    l.l = N(v[3])
    l.r = N(v[4])
    return r

def main():
    v = list(map(int, input().split()))
    r = b(v)
    print("Preorder traversal:")
    print(" ".join(map(str, p(r))))
    print("Inorder traversal:")
    print(" ".join(map(str, i(r))))
    print("Postorder traversal:")
    print(" ".join(map(str, q(r))))

if __name__ == "__main__":
    main()
```

---

### Java Code:

```java
import java.util.Scanner;

class Node {
    int data;
    Node left, right;

    Node(int item) {
        data = item;
        left = right = null;
    }
}

class Main {
    static Node newNode(int data) {
        Node node = new Node(data);
        node.left = node.right = null;
        return node;
    }

    static void printPostorder(Node node) {
        if (node == null)
            return;

        // first recur on left subtree
        printPostorder(node.left);

        // then recur on right subtree
        printPostorder(node.right);

        // now deal with the node
        System.out.print(node.data + " ");
    }

    static void printInorder(Node node) {
        if (node == null)
            return;

        // first recur on left child
        printInorder(node.left);

        // then print the data of node
        System.out.print(node.data + " ");

        // now recur on right child
        printInorder(node.right);
    }

    static void printPreorder(Node node) {
        if (node == null)
            return;

        // first print data of node
        System.out.print(node.data + " ");

        // then recur on left subtree
        printPreorder(node.left);

        // now recur on right subtree
        printPreorder(node.right);
    }

    public static void main(String[] args) {
        int[] arr = new int[5];
        Scanner sc = new Scanner(System.in);
        for (int i = 0; i < 5; i++)
            arr[i] = sc.nextInt();

        Node root = newNode(arr[0]);
        root.left = newNode(arr[1]);
        root.right = newNode(arr[2]);
        root.left.left = newNode(arr[3]);
        root.left.right = newNode(arr[4]);

        System.out.println("Preorder traversal:");
        printPreorder(root);

        System.out.println("\nInorder traversal:");
        printInorder(root);

        System.out.println("\nPostorder traversal:");
        printPostorder(root);
    }
}
```

---

### Explanation:

1. **Tree Structure**:
   - We create a `Node` class to represent the nodes in the binary tree, each having a `value`, `left`, and `right` child.
   - The family tree follows the structure defined by the rules: one elder with two children, and the first child has two children, while the second child is a leaf node.

2. **Tree Traversals**:
   - **Preorder Traversal**: The node is processed before its children.
   - **Inorder Traversal**: The node is processed between its left and right children.
   - **Postorder Traversal**: The node is processed after its children.

3. **Traversal Functions**:
   - `p(n)`: Preorder traversal function.
   - `i(n)`: Inorder traversal function.
   - `q(n)`: Postorder traversal function.

4. **Tree Construction**:
   - `b(v)`: Function to construct the binary tree based on the 5 values.

5. **Main Logic**:
   - The main function reads 5 integers as input, constructs the binary tree, and prints the tree traversals in the required format.

---

### Time Complexity:
- The time complexity of each traversal function (preorder, inorder, postorder) is O(n), where `n` is the number of nodes in the tree, which is always 5 in this problem.

---

### Space Complexity:
- The space complexity is O(n) due to the recursion stack for the tree traversal.
