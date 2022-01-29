# Subsets Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/subsets/

## Problem Description

*The description of the "Subsets" problem is as follows:*

Given an integer array `nums` of **unique** elements, return *all possible subsets (the power set).*

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

**Constraints**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**.


## Solution

Below is my working solution for the problem in Leetcode:

```
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> subset = new ArrayList<>();
        if(nums.length == 1){
            result.add(subset);
            List<Integer> nonEmptySubset = new ArrayList<>();
            nonEmptySubset.add(nums[0]);
            result.add(nonEmptySubset);
            return result;
        }
        
        createSubsets(nums, result, subset, 0);
        
        return result;
    }
    
    public void createSubsets(int[] nums, List<List<Integer>> result, List<Integer> subset, int start){
        List<Integer> addedSubset = new ArrayList<>();
        for(int k = 0; k < subset.size(); k++){
            addedSubset.add(subset.get(k));
        }
        result.add(addedSubset);
        if(start != nums.length){
            for(int i = start; i < nums.length; i++){
                subset.add(nums[i]);
                createSubsets(nums, result, subset, i+1);
                subset.remove(subset.size()-1);
            }
        }
        
    }
}
```
This solution has a runtime of approximately 0-2ms and a memory usage of approximately 42-44MB. 
