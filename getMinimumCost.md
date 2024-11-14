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



# Pyton Solution

```
def getMinimumCost(cost, featureAvailability):
    n = len(cost)
    feature_a = []
    feature_b = []
    both_features = []
    
    for i in range(n):
        if featureAvailability[i] == "11":
            both_features.append(cost[i])
        elif featureAvailability[i] == "10":
            feature_b.append(cost[i])
        elif featureAvailability[i] == "01":
            feature_a.append(cost[i])
    
    feature_a.sort()
    feature_b.sort()
    both_features.sort()
    
    prefix_a = [0] * (len(feature_a) + 1)
    prefix_b = [0] * (len(feature_b) + 1)
    prefix_both = [0] * (len(both_features) + 1)
    
    for i in range(1, len(feature_a) + 1):
        prefix_a[i] = prefix_a[i - 1] + feature_a[i - 1]
    for i in range(1, len(feature_b) + 1):
        prefix_b[i] = prefix_b[i - 1] + feature_b[i - 1]
    for i in range(1, len(both_features) + 1):
        prefix_both[i] = prefix_both[i - 1] + both_features[i - 1]
    
    def find_min_cost_for_k(k):
        total_a = len(feature_a) + len(both_features)
        total_b = len(feature_b) + len(both_features)
        
        if total_a < k or total_b < k:
            return -1
        
        min_cost = float('inf')
        
        for both_count in range(min(k + 1, len(both_features) + 1)):
            remaining_a = k - both_count
            remaining_b = k - both_count
            
            if remaining_a > len(feature_a) or remaining_b > len(feature_b):
                continue
            
            current_cost = prefix_both[both_count]
            current_cost += prefix_a[remaining_a]
            current_cost += prefix_b[remaining_b]
            
            min_cost = min(min_cost, current_cost)
        
        return min_cost if min_cost != float('inf') else -1
    
    result = []
    for k in range(1, n + 1):
        result.append(find_min_cost_for_k(k))
    
    return result

if _name_ == '_main_':
    n = int(input())
    cost = []
    for _ in range(n):
        cost.append(int(input()))
    
    m = int(input())
    featureAvailability = []
    for _ in range(m):
        featureAvailability.append(input())
    
    result = getMinimumCost(cost, featureAvailability)
    for value in result:
        print(value)
```
