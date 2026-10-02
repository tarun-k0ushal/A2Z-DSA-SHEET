# 3Sum

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

 

 **Example 1:** 

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

```

 **Example 2:** 

```
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.

```

 **Example 3:** 

```
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.

```

 

 **Constraints:** 

- 3 <= nums.length <= 3000
- -105 <= nums[i] <= 105

## Solution

**Language:** C++  
**Runtime:** 51 ms (beats 40.73%)  
**Memory:** 33.2 MB (beats 12.81%)  
**Submitted:** 2026-10-02T17:38:13.878Z  

```cpp
class Solution {
    vector<vector<int>> result;

    void twosum(vector<int>& nums, int target, int i, int j) {

        while (i < j) {

            if (nums[i] + nums[j] > target) {
                j--;
            }
            else if (nums[i] + nums[j] < target) {
                i++;
            }
            else {

                result.push_back({-target, nums[i], nums[j]});

                while (i < j && nums[i] == nums[i + 1]) i++;
                while (i < j && nums[j] == nums[j - 1]) j--;

                i++;
                j--;
            }
        }
    }

public:
    vector<vector<int>> threeSum(vector<int>& nums) {

        int n = nums.size();

        if (n < 3)
            return {};

        result.clear();

        sort(nums.begin(), nums.end());

        for (int i = 0; i < n - 2; i++) {

            if (i > 0 && nums[i] == nums[i - 1])
                continue;

            int target = -nums[i];

            twosum(nums, target, i + 1, n - 1);
        }

        return result;
    }
};
```

---

[View on LeetCode](https://leetcode.com/problems/3sum/)