# 2044. Count Number of Maximum Bitwise-OR Subsets

## Problem Statement

Given an integer array `nums`, find the **maximum possible bitwise OR** of a subset of `nums` and return the **number of different non-empty subsets** with the maximum bitwise OR.

- An array `a` is a subset of array `b` if `a` can be obtained from `b` by deleting some (possibly zero) elements.
- Two subsets are considered different if the **indices** of the elements chosen are different (even if values are the same).
- The bitwise OR of an array `a` is defined as `a[0] OR a[1] OR ... OR a[a.length - 1]`.

---

## Examples

### Example 1
**Input:**  
`nums = [3, 1]`  
**Output:**  
`2`  
**Explanation:**  
Maximum bitwise OR is 3. Two subsets with OR 3:
- `[3]`
- `[3, 1]`

---

### Example 2
**Input:**  
`nums = [2, 2, 2]`  
**Output:**  
`7`  
**Explanation:**  
All non-empty subsets have OR = 2.  
Total non-empty subsets = 2³ - 1 = 7.

---

### Example 3
**Input:**  
`nums = [3, 2, 1, 5]`  
**Output:**  
`6`  
**Explanation:**  
Maximum bitwise OR is 7. Subsets with OR 7:
- `[3, 5]`
- `[3, 1, 5]`
- `[3, 2, 5]`
- `[3, 2, 1, 5]`
- `[2, 5]`
- `[2, 1, 5]`

---

## Constraints

- `1 <= nums.length <= 16`
- `1 <= nums[i] <= 10⁵`

---

## Solution Approach

1. **Calculate Maximum Bitwise OR:**  
   - Use bitwise OR on all elements to get the maximal value (`maxOR`).
2. **Enumerate All Subsets:**  
   - For each possible subset (except the empty set), compute its bitwise OR.
   - Count how many subsets' OR equals `maxOR`.
3. **Complexity:**  
   - Since `nums.length <= 16`, total subsets = \(2^{16}\), which is feasible.

---

## Solution Code

```cpp name=Solution.cpp
class Solution {
public:
    int countMaxOrSubsets(vector<int>& nums) {
        int n = nums.size();
        int maxOR = 0;
        
        // Find the maximum possible OR
        for (int i = 0; i < n; i++) {
            maxOR |= nums[i];
        }

        int count = 0;
        int totalSubsets = 1 << n;

        // Enumerate all non-empty subsets
        for (int mask = 1; mask < totalSubsets; mask++) {
            int currOR = 0;
            for (int i = 0; i < n; i++) {
                if (mask & (1 << i)) {
                    currOR |= nums[i];
                }
            }
            if (currOR == maxOR) {
                count++;
            }
        }

        return count;
    }
};
```

