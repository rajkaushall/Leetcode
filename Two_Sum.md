# Two Sum

**Difficulty:** Easy  
**Topics:** Array, Hash Table

---

## Problem

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you **may not use the same element twice**.

You can return the answer in **any order**.

---

## Example 1

**Input:**  
`nums = [2,7,11,15]`, `target = 9`  
**Output:**  
`[0,1]`  
**Explanation:**  
Because `nums[0] + nums[1] == 9`, we return `[0, 1]`.

---

## Example 2

**Input:**  
`nums = [3,2,4]`, `target = 6`  
**Output:**  
`[1,2]`

---

## Example 3

**Input:**  
`nums = [3,3]`, `target = 6`  
**Output:**  
`[0,1]`

---

## Constraints

- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`

---

## Brute Force Approach (Pseudocode)

```text
For i from 0 to length of nums - 1:
    For j from i + 1 to length of nums - 1:
        If nums[i] + nums[j] == target:
            Return [i, j]
```

**Explanation:**  
- Loop through every pair of indices `(i, j)` in the array where `i < j`.
- If the sum of `nums[i]` and `nums[j]` equals `target`, return their indices.
- Time Complexity: O(n²)


## Optimal Approach: Hashing (Pseudocode)

```text
Create an empty hash map   called num_to_index

For i from 0 to length of nums - 1:
    complement = target - nums[i]
    If complement exists in num_to_index:
        Return [num_to_index[complement], i]
    Else:
        num_to_index[nums[i]] = i
```
## Optimal Approach: Hashing (C++ Code)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mpp;
        for (int i = 0; i < nums.size(); i++) {
            int comp = target - nums[i];
            // Check if complement exists in map
            if (mpp.count(comp)) {
                return {mpp[comp], i};
            }
            // Store current number and its index
            mpp[nums[i]] = i;
        }
        return {}; // No solution found (should not happen per constraints)
    }
};
```

**Explanation:**  
- For each element, calculate its complement (`target - nums[i]`).
- Check if the complement is already stored in the hash map.
- If found, return the indices: the index of the complement and the current index.
- Otherwise, store the current number and its index in the hash map.
- This approach has time complexity O(n) and space complexity O(n).
- In unordered map best/avg. case will be O(n) and worst will be O(n^2). In case of map TC will be O(n).

  # Two Sum: Two Pointer Technique

## Approach Explanation

The **two-pointer technique** is a common pattern used to solve problems involving sorted arrays. For the Two Sum problem, this approach finds two numbers that add up to a given target. However, since the original array may not be sorted, and we need to return the **original indices**, we must take extra care.

### Steps

1. **Store Numbers with Indices:**  
   First, pair each number with its original index as `(value, index)`.

2. **Sort the Array:**  
   Sort the array of pairs based on the numbers, not their indices.

3. **Apply Two-Pointer Technique:**  
   - Place one pointer (`left`) at the beginning, and another (`right`) at the end of the sorted array.
   - Calculate the sum of the numbers at these two pointers.
   - If the sum is **less than** the target, move the `left` pointer forward to increase the sum.
   - If the sum is **greater than** the target, move the `right` pointer backward to decrease the sum.
   - If the sum **equals** the target, return the original indices.

### Why this works

By sorting, we can efficiently search for a pair that sums to the target in O(n) time after sorting (which itself is O(n log n)).  
Storing indices ensures correct output, since sorting would otherwise lose their positions.

---

## Pseudocode

```text
Let arr be an array of (value, index) pairs
Sort arr by value
left = 0, right = length(arr) - 1
While left < right:
    sum = arr[left].value + arr[right].value
    If sum == target:
        Return [arr[left].index, arr[right].index]
    Else if sum < target:
        left = left + 1
    Else:
        right = right - 1
Return []
```

---

## C++ Implementation

```cpp
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        // Pair each number with its index
        vector<pair<int, int>> arr;
        for (int i = 0; i < nums.size(); ++i)
            arr.push_back({nums[i], i});
        // Sort pairs by value
        sort(arr.begin(), arr.end());
        int left = 0, right = nums.size() - 1;
        while (left < right) {
            int sum = arr[left].first + arr[right].first;
            if (sum == target)
                return {arr[left].second, arr[right].second};
            else if (sum < target)
                ++left;
            else
                --right;
        }
        return {};
    }
};
```

---

## Complexity

- **Time Complexity:** O(n log n) (due to sorting)
- **Space Complexity:** O(n) (for the auxiliary array)

  
