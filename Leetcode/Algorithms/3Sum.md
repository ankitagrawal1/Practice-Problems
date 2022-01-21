# 3Sum Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/3sum/

## Problem Description

*The description of the "3Sum" problem is as follows:*

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1**

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

**Example 2**

```
Input: nums = []
Output: []
```

**Example 3**

```
Input: nums = [0]
Output: []
```

**Constraints**

- `0 <= nums.length <= 3000`
- `-(10^5) <= nums[i] <= 10^5`

## Solution

In order to reach this solution, I had to refer to the three hints offered in the problem, and the hints were as follows:

**Hint 1**: So, we essentially need to find three numbers x, y, and z such that they add up to the given value. If we fix one of the numbers say x, we are left with the two-sum problem at hand!

**Hint 2**: For the two-sum problem, if we fix one of the numbers, say `x`, we have to scan the entire array to find the next number `y` which is `value - x` where `value` is the input parameter. Can we change our array somehow so that this search becomes faster?

**Hint 3**: The second train of thought for two-sum is, without changing the array, can we use additional space somehow? Like maybe a hash map to speed up the search?

Below is my working solution for the problem in Leetcode after referring to the hints above. The main function being called is `threeSum(int[] nums)`, while `sortTriple(int[] triple)` serves as a helper function:

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> triples = new ArrayList<>();
        Set<List<Integer>> uniqueTriples = new HashSet<>();
        if(nums.length <= 3){
            if(nums.length == 3 && nums[0] + nums[1] + nums[2] == 0){
                List<Integer> list = new ArrayList<>();
                list.add(nums[0]);
                list.add(nums[1]);
                list.add(nums[2]);
                triples.add(list);
            }
            return triples;
        }
        Map<Integer, Integer> map = new HashMap<>();
        for(int k = 0; k < nums.length; k++){
            int result = map.getOrDefault(nums[k], 0) + 1;
            map.put(nums[k], result);
        }
        for(int i = 0; i < nums.length-1; i++){
            for(int m = i+1; m < nums.length; m++){
                int value = 0-nums[i]-nums[m];
                int exists = map.getOrDefault(value, 1000000);
                if(exists != 1000000){
                    if(value == nums[i] && map.get(value) < 2 || value == nums[m] && map.get(value) < 2 || value == nums[i] && value == nums[m] && map.get(value) < 3){
                        continue;
                    } else {
                        int[] list = {nums[i], nums[m], value};
                        uniqueTriples.add(sortTriple(list));
                    }
                }
            }
        }
        for(List<Integer> list: uniqueTriples){
            triples.add(list);
        }
        return triples;
    }
    
    public List<Integer> sortTriple(int[] triple){
        List<Integer> list = new ArrayList<>();
        int firstVal = triple[0];
        int secondVal = triple[1];
        int thirdVal = triple[2];
        
        if(firstVal <= secondVal && firstVal <= thirdVal){
            list.add(firstVal);
            if(secondVal < thirdVal){
                list.add(secondVal);
                list.add(thirdVal);
            } else {
                list.add(thirdVal);
                list.add(secondVal);
            }
        } else if (secondVal <= firstVal && secondVal <= thirdVal){
            list.add(secondVal);
            if(firstVal < thirdVal){
                list.add(firstVal);
                list.add(thirdVal);
            } else {
                list.add(thirdVal);
                list.add(firstVal);
            }
        } else {
            list.add(thirdVal);
            if(firstVal < secondVal){
                list.add(firstVal);
                list.add(secondVal);
            } else {
                list.add(secondVal);
                list.add(firstVal);
            }
        }
        return list;
    }
}
```
This solution has a runtime of approximately 1500-2500ms and a memory usage of approximately 200-300MB. 
