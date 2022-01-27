# Permutations Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/permutations/

## Problem Description

*The description of the "Permutations" problem is as follows:*

Given an array nums of distinct integers, return *all the possible permutations*. You can return the answer **in any order**.

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**Example 2:**

```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

**Example 3:**

```
Input: nums = [1]
Output: [[1]]
```

**Constraints**

- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- All the integers of `nums` are **unique**.

## Solution

Below is my working solution for the problem in Leetcode. The main function being called is `permute(int[] nums)`, while `createPermutations(List<List<Integer>> list, List<Integer> currentResult, List<Integer> uniqueNums)` is a helper function:

```
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        List<Integer> result = new ArrayList<>();
        if(nums.length == 1){
            result.add(nums[0]);
            list.add(result);
            return list;
        }
        List<Integer> uniqueNums = new ArrayList<>();
        for(int i = 0; i < nums.length; i++){
            uniqueNums.add(nums[i]);
        }
        createPermutations(list, result, uniqueNums);
        return list;
        
    }
    
    public void createPermutations(List<List<Integer>> list, List<Integer> currentResult, List<Integer> uniqueNums){
        if(uniqueNums.size() == 1){
            currentResult.add(uniqueNums.get(0));
            List<Integer> completePerm = new ArrayList<>();
            for(int f = 0; f < currentResult.size(); f++){
                completePerm.add(currentResult.get(f));
            }
            list.add(completePerm);
            currentResult.remove(currentResult.size()-1);
        } else {
            int numOfVals = uniqueNums.size();
            for(int i = 0; i < numOfVals; i++){
                int value = uniqueNums.get(i);
                currentResult.add(value);
                uniqueNums.remove(i);
                createPermutations(list, currentResult, uniqueNums);
                currentResult.remove(currentResult.size()-1);
                uniqueNums.add(i, value);
            }
        }
    }
}
```
This solution has a runtime of approximately 1-5 ms and a memory usage of approximately 42-45MB. 
