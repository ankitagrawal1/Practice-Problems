# Two Sum Solution

This problem is available on LeetCode, and can be found through the following link: https://leetcode.com/problems/two-sum/

## Problem Description

The description of the "Two Sum" problem is as follows:

*Given an array of integers, return indices of the two numbers such that they add up to a specific target. You may assume that each input would have exactly one solution, and you may not use the same element twice.*

**Example:**

*Given nums = [2, 7, 11, 15], target = 9,*

*Because nums[0] + nums[1] = 2 + 7 = 9, return [0, 1].*

## Solution

Upon a first look at the problem, I recognized that while the example included values in numerical order, the problem did not explicitly state that the provided arrays would be in ascending order. Therefore, I had to assume that my solution would need to account for arrays with values in any order.

### Initial Solution

If the array values can be in any order, then I thought that the most straightforward way to get two values that would meet the target sum would be use an inner/outer loop structure. The outer loop would track one index, and the inner loop would track the other. With this method, I could go through each possible combination until the correct indices are reached. Those values could immediately be returned in another array, and I would not need to loop through the rest of the array.

The following solution successfully passed LeetCodes's submission system:

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int first = 0; first < nums.length; first++){
            for(int last = first+1; last < nums.length; last++){
                int sum = nums[first] + nums[last];
                if(sum == target){
                    int result[] = {first, last};
                    return result;
                }
            }
        }
        int noPair[] = new int[2];
        return noPair;
    }
}
```

According to LeetCode, the solution had a runtime of 19 ms and was faster than 30.30% of Java online submissions for the problem at the time.

### Possible Improvements

While the solution works, it is not as efficient as it could be. In the worst case scenario, I would have to check every possible array index pairing until either the target sum is achieved or the empty array is returned (in the case that no two indices have values summing to the target array value).

Hence, one potential improvement would be to implement a sorting algorithm prior to searching for values. Once the values are sorted, I could set starting index values at the beginning and end of the array. If the sum is smaller than the target sum, I would increment the beginning index value, and if the sum is larger than the target, I would decrement the ending index value. Using a sorting algorithm such as a binary sort could take ```nlog(n)``` time, and this updated method of searching the array would have a linear worst-case search time. This means that the entire solution would have take less than Big-Oh of n<sup>2</sup> to finish running, which is much more efficient that the initial solution written above.

Additionally, I had my solution account for situations where there may be no pair of indices that achieves the target sum (something outside of the scope of the original problem statement). However, if I wanted to limit the solution to arrays that definitively had one solution, the extra return statement at the end with an empty array could be removed. I could then also alter the loop structure to ensure that the return statement is outside of the if-statement by potentially reframing the if-statement to an if-else condition that checks if ```sum != target```.
