# Reverse Integer Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/reverse-integer

## Problem Description

The description of the "Reverse Integer" problem is as follows:

Given a signed 32-bit integer `x`, return `x` *with its digits reversed*. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-(2^31), (2^31) - 1]`, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

**Example 1**

```
Input: x = 123
Output: 321
```

**Example 2**

```
Input: x = -123
Output: -321
```

**Example 3**

```
Input: x = 120
Output: 21
```

**Constraints**

- `-(2^31) <= x <= (2^31) - 1`

## Solution

Below is my working solution for the problem in Leetcode:

```
class Solution {
    public int reverse(int x) {
        int mathMax = (int)Math.pow(2,31) - 1;
        String mathMaxString = mathMax + "";
        int mathMin = (-1) * (int)Math.pow(2,31);
        String mathMinString = mathMin + "";
        String xString = x + "";
        if(xString.length() <= 1){
            return x;
        }
        int starter = 0;
        int multiplier = 1;
        if(x < 0){
            xString = xString.substring(1);
            multiplier = -1;
        }
        int oppDigit = xString.length()-1;
        if(xString.length() == 2){
            String firstChar = xString.charAt(0) + "";
            String secondChar = xString.charAt(1) + "";
            xString = secondChar + firstChar;
        }
        else{
            for(int i = 0; i < xString.length()/2; i++){
                String firstChar = xString.charAt(i) + "";
                xString = xString.substring(starter, i) + xString.charAt(oppDigit) + xString.substring(i+1, oppDigit) + firstChar + xString.substring(oppDigit+1);
                oppDigit--;
            }
        }
        String negativeXString = "-" + xString;
        if((multiplier > 0 && xString.length() > mathMaxString.length()) || (multiplier < 0 && xString.length() + 1 > mathMinString.length()) ){
            return 0;
        }
        if((multiplier > 0 && xString.length() == mathMaxString.length()) || (multiplier < 0 && xString.length() + 1 == mathMinString.length()) ){
            String toCompare = mathMaxString;
            int start = 0;
            int negBump = 0;
            if(multiplier < 0){
                toCompare = mathMinString;
                start = 1;
                negBump = 1;
            }
            for(int i = start; i < toCompare.length(); i++){
                if(Integer.parseInt(xString.substring(i, i+1)) > Integer.parseInt(toCompare.substring(negBump + i, negBump+i+1)) ){
                    return 0;
                }
                else if(Integer.parseInt(xString.substring(i, i+1)) < Integer.parseInt(toCompare.substring(negBump + i, negBump+i+1)) ){
                    break;
                }
            }
        }
        return Integer.parseInt(xString) * multiplier;
    }
}
```
This solution has a runtime of approximately 36-41ms and a memory usage of approximately 41-42MB. 
