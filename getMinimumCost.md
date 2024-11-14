### Problem Statement:

Given **n** machine learning models, each with an associated **cost** and **feature compatibility**. The **cost** of the \(i\)-th model is specified by the array element **cost[i]**. Additionally, each model is characterized by a binary string, **featureAvailability[i]**, indicating its suitability for two distinct features:

- If **featureAvailability[i] = "00"**, it means the model is not equipped for either of the features.
- If **featureAvailability[i] = "01"**, the model is designed for **feature A** but not for **feature B**.
- If **featureAvailability[i] = "10"**, the model is designed for **feature B** but not for **feature A**.
- If **featureAvailability[i] = "11"**, the model is suitable for **both features**.

A set of models is considered **k-capable** if the number of models in that set suitable for **feature A** and the number of models suitable for **feature B** are both greater than or equal to **k**.

For each value of **k**, ranging from 1 to **n**, the goal is to determine the **minimum cost** required to assemble a set of **k-capable** machine learning models. The task is to return an array of **n** integers, where the \(i\)-th integer denotes the minimum cost of acquiring a set of **i-capable** models. If there exists no feasible combination of **i-capable** models, the corresponding \(i\)-th integer will be **-1**.

### Example  

Given:
- \( n = 6 \)  
- \( \text{cost} = [3, 6, 9, 1, 2, 5] \)  
- \( \text{featureAvailability} = ["10", "01", "11", "01", "11", "10"] \)  

| \( k \) | Optimal Set           | Feature 1 Compatible | Feature 2 Compatible | Cost                 |
|---------|------------------------|-----------------------|-----------------------|----------------------|
| 1       | [5]                   | [5]                  | [5]                  | 2                    |
| 2       | [1, 4, 5]             | [1, 5]               | [4, 5]               | 3 + 1 + 2 = 6        |
| 3       | [1, 3, 4, 5]          | [1, 3, 5]            | [3, 4, 5]            | 3 + 9 + 1 + 2 = 15   |
| 4       | [1, 2, 3, 4, 5, 6]    | [1, 3, 5, 6]         | [2, 3, 4, 5]         | 3 + 6 + 9 + 1 + 2 + 5 = 26 |

For \( k \geq 5 \), there will be no capable set.  
**Answer**: \([2, 6, 15, 26, -1, -1]\).

### Function Description  
Complete the function **getMinimumCost** in the editor below.

**getMinimumCost** has the following parameters:
- **int cost[n]**: the cost of machine learning models
- **string featureAvailability[n]**: the compatibility string of models indicating its suitability for two features

**Returns**:
- **int[n]**: the \(i^{th}\) integer is the minimum cost of a set of \(i\)-capable models

### Constraints
- \(1 \leq n \leq 10^5\)
- \(1 \leq cost[i] \leq 10^4\)
- It is guaranteed that **featureAvailability[i]** is a binary string of length 2.

---

### Input Format for Custom Testing

- The first line contains an integer, **n**, the number of machine learning models.
- Each of the next **n** lines contains an integer **cost[i]**.
- The next line contains an integer, **n**, the number of models.
- Each of the next **n** lines contains a string **featureAvailability[i]**.

### Sample Input 1:

```
4
5
6
10
1
4
10
01
11
00
```

### Sample Output 1:

```
10
21
-1
-1
```

### Explanation:

| \( k \) | Optimal Set           | Feature 1 Compatible | Feature 2 Compatible | Cost                 |
|---------|------------------------|-----------------------|-----------------------|----------------------|
| 1       | [3]                   | [3]                  | [3]                  | 10                   |
| 2       | [1, 2, 3]             | [1, 3]               | [2, 3]               | 5 + 6 + 10 = 21      |

For \( k \geq 3 \), there will be no capable set.
Hence, the answer is [10,21,-1,-1].


### Sample Input 2:

```
2
1
1
2
10
10
```

### Sample Output 2:

```
-1
-1
```
### Explanation:

There is no possible way of forming a k-capable set for all k from 1 to n.
