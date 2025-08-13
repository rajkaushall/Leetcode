# 2210. Count Hills and Valleys in an Array

## Problem Statement

You are given a 0-indexed integer array `nums`. An index `i` is part of a **hill** in `nums` if the closest non-equal neighbors of `i` are smaller than `nums[i]`. Similarly, an index `i` is part of a **valley** in `nums` if the closest non-equal neighbors of `i` are larger than `nums[i]`. Adjacent indices `i` and `j` are part of the same hill or valley if `nums[i] == nums[j]`.

**Note:** For an index to be part of a hill or valley, it must have a non-equal neighbor on both the left and right of the index.

Return the number of hills and valleys in `nums`.

---

### Example 1

**Input:**  
`nums = [2,4,1,1,6,5]`  
**Output:**  
`3`  
**Explanation:**
- Index 1 (`4`) is a hill (neighbors: `2` and `1`).
- Index 2 and 3 (`1,1`) form a valley (neighbors: `4` and `6`).
- Index 4 (`6`) is a hill (neighbors: `1` and `5`).
- Total hills and valleys = 3.

### Example 2

**Input:**  
`nums = [6,6,5,5,4,1]`  
**Output:**  
`0`  
**Explanation:**  
No hills or valleys as neighbors do not satisfy conditions.

---

## Constraints

- `3 <= nums.length <= 100`
- `1 <= nums[i] <= 100`

---

## Solution Approach

- Iterate through array and, for each index, skip over any plateaus (consecutive equal values).
- For each index, find the closest non-equal neighbors on the left and right.
- Count as a hill if current value is greater than both neighbors, or as a valley if less than both.
- Skip over plateaus by moving to the next different value after counting.

---

## Solution Code

```cpp name=Solution.cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int countHillValley(vector<int>& nums) {
        int res = 0;
        int n = nums.size();
        for (int i = 1; i < n-1; ) {
            int left = i-1;
            int right = i+1;
            // Move left to the closest not-equal neighbor
            while (left >= 0 && nums[left] == nums[i]) left--;
            // Move right to the closest not-equal neighbor
            while (right < n && nums[right] == nums[i]) right++;
            if (left >= 0 && right < n) {
                if (nums[i] > nums[left] && nums[i] > nums[right])
                    res++;
                if (nums[i] < nums[left] && nums[i] < nums[right])
                    res++;
            }
            i = right; // Skip all same values, only check once per plateau
        }
        return res;
    }
};
```

---

