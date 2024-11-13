# LFU Cache Implementation

This repository contains a Python implementation of the **Least Frequently Used (LFU) Cache** with specific functionalities for handling `GET` and `PUT` operations, accommodating a defined cache size. This implementation is optimized for performance and includes logic to handle ties between frequencies by evicting the least recently used item in such cases.

## Problem Description

The LFU Cache needs to support two types of queries:

1. **GET** - Attempts to retrieve the value associated with a given key.
   - If the key is present, it returns the value.
   - If the key is not present, it returns `-1`.

2. **PUT** - Inserts or updates a key-value pair in the cache.
   - If the cache exceeds its maximum capacity, the least frequently used key is removed.
   - If there is a tie in frequencies, the least recently used key among those is removed.

The output for a series of queries will be an array of integers representing the results of each `GET` operation.

### Constraints
- `2 ≤ cacheSize ≤ 100`
- `1 ≤ q ≤ 10^5` (number of queries)
- Key and value ranges are provided as integers.

## Sample Usage

**Input:**
```
cacheSize = 2
queries = [
    "PUT 1 1",
    "PUT 2 2",
    "GET 1",
    "PUT 3 3",
    "GET 2"
]
```

**Expected Output:**
```
[1, -1]
```

## Solution Code

```python
from collections import defaultdict, OrderedDict

class LFUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.keyToValue = {}  # Stores the key-value pairs
        self.keyToFreq = defaultdict(int)  # Tracks the frequency of each key
        self.freqToKeys = defaultdict(OrderedDict)  # Maps frequency to keys in an ordered way
        self.minFreq = 0  # Tracks the minimum frequency in the cache

    def get(self, key: int) -> int:
        if key not in self.keyToValue:
            return -1
        freq = self.keyToFreq[key]
        # Update frequency mappings
        self.keyToFreq[key] += 1
        del self.freqToKeys[freq][key]
        self.freqToKeys[freq + 1][key] = True
        # Update minFreq if necessary
        if freq == self.minFreq and not self.freqToKeys[freq]:
            self.minFreq += 1
        return self.keyToValue[key]

    def put(self, key: int, value: int) -> None:
        if self.capacity <= 0:
            return
        if key in self.keyToValue:
            # Update the value and frequency
            self.keyToValue[key] = value
            self.get(key)  # Update frequency as if it was accessed
            return
        if len(self.keyToValue) >= self.capacity:
            # Evict the least frequently used item
            evictKey, _ = self.freqToKeys[self.minFreq].popitem(last=False)
            del self.keyToValue[evictKey]
            del self.keyToFreq[evictKey]
        # Add the new key-value pair
        self.keyToValue[key] = value
        self.keyToFreq[key] = 1
        self.freqToKeys[1][key] = True
        self.minFreq = 1  # Reset min frequency to 1

def process_queries(cachesize, queries):
    cache = LFUCache(cachesize)
    results = []
    for query in queries:
        parts = query.split()
        if parts[0] == "PUT":
            cache.put(int(parts[1]), int(parts[2]))
        elif parts[0] == "GET":
            results.append(cache.get(int(parts[1])))
    return results

if __name__ == "__main__":
    cachesize = int(input())
    n = int(input())
    queries = [input().strip() for _ in range(n)]
    output = process_queries(cachesize, queries)
    print(" ".join(map(str, output)))
```

## Explanation of the Code

- **LFUCache Class:** This class implements the LFU cache with methods for `GET` and `PUT`.
  - **`get(key: int)`**: Increases the frequency of the key if it exists and returns the value, otherwise returns `-1`.
  - **`put(key: int, value: int)`**: Adds or updates a key-value pair in the cache, and evicts the least frequently used key if necessary.
- **`process_queries` Function:** Processes a series of `PUT` and `GET` commands and records the output for each `GET`.

## Example Execution

For `cacheSize = 2` and `queries = ["PUT 1 1", "PUT 2 2", "GET 1", "PUT 3 3", "GET 2"]`, the process is as follows:

| Query       | Cache (State)         | Result |
|-------------|------------------------|--------|
| PUT 1 1     | {1: 1}                 | -      |
| PUT 2 2     | {1: 1, 2: 2}           | -      |
| GET 1       | {1: 1 (used), 2: 2}    | 1      |
| PUT 3 3     | {1: 1 (used), 3: 3}    | -      |
| GET 2       | {1: 1, 3: 3}           | -1     |

Result: `[1, -1]`

## Explanation of Eviction Strategy

1. When adding a new key, if the cache is full, the least frequently used key is evicted.
2. If multiple keys share the lowest frequency, the least recently used key among them is evicted.

This approach maintains a balanced performance for frequent operations due to the efficient use of data structures (`OrderedDict` and `defaultdict`).

## Constraints and Complexity

- **Time Complexity**: Average O(1) for `GET` and `PUT` due to efficient dictionary and ordered dictionary usage.
- **Space Complexity**: O(capacity) for storing up to the maximum number of key-value pairs defined by `cacheSize`.

