# Heaters Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/heaters/

## Problem Description

*The description of the "Heaters" problem is as follows:*

Winter is coming! During the contest, your first job is to design a standard heater with a fixed warm radius to warm all the houses.

Every house can be warmed, as long as the house is within the heater's warm radius range. 

Given the positions of `houses` and `heaters` on a horizontal line, return *the minimum radius standard of heaters so that those heaters could cover all houses.*

**Notice** that all the `heaters` follow your radius standard, and the warm radius will the same.

**Example 1:**

```
Input: houses = [1,2,3], heaters = [2]
Output: 1
Explanation: The only heater was placed in the position 2, and if we use the radius 1 standard, then all the houses can be warmed.
```

**Example 2:**

```
Input: houses = [1,2,3,4], heaters = [1,4]
Output: 1
Explanation: The two heater was placed in the position 1 and 4. We need to use radius 1 standard, then all the houses can be warmed.
```

**Example 3:**
```
Input: houses = [1,5], heaters = [2]
Output: 3
```

**Constraints**

- `1 <= houses.length, heaters.length <= 3 * (10^4)`
- `1 <= houses[i], heaters[i] <= (10^9)`

## Solution

Below is my working solution for the problem in Leetcode:

```
class Solution {
    public int findRadius(int[] houses, int[] heaters) {
        // Base Cases
        if(heaters.length == 1){
            int heat = heaters[0];
            if(houses.length == 1){
                return Math.abs(houses[0] - heat);
            }
            Arrays.sort(houses);
            return Math.max(Math.abs(houses[0]-heat), Math.abs(houses[houses.length-1]-heat));
        }
        if(houses.length == 1){
            int radius = houses[0];
            for(int i = 0; i < heaters.length; i++){
                radius = Math.min(radius, Math.abs(heaters[i]-houses[0]));
            }
            return radius;
        }
        
        // Sort Arrays
        Arrays.sort(houses);
        Arrays.sort(heaters);
        
        // Determine first radius value
        int firstPointer = 0;
        int secondPointer = 1;
        while(secondPointer < heaters.length && heaters[secondPointer] < houses[0]){
            firstPointer++;
            secondPointer++;
        }
        int radius = Math.min(Math.abs(houses[0]-heaters[firstPointer]), Math.abs(houses[0]-heaters[secondPointer])) ;
        
        // Find Max Radius
        int startingIndex = 1;
        while(startingIndex < houses.length){
            int dist = houses[startingIndex];
            boolean breakWhile = false;
            while(dist >= heaters[secondPointer]){
                if(secondPointer + 1 == heaters.length){
                    breakWhile = true;
                    break;
                }
                firstPointer++;
                secondPointer++;
            }
            if(breakWhile){
                break;
            }
            int shortestDist = Math.min(heaters[secondPointer]-dist, dist-heaters[firstPointer]);
            radius = Math.max(radius, shortestDist);
            startingIndex++;
        }
        if(startingIndex != houses.length){
            radius = Math.max(radius, Math.abs(houses[houses.length-1]-heaters[secondPointer]));
        }
        
        return radius;
    }
}
```
This solution has a runtime of approximately 11-18ms and a memory usage of approximately 54-55MB. 
