# String to Integer (atoi) Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/string-to-integer-atoi/

## Problem Description

The description of the "String to Integer (atoi)" problem is as follows:

Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer (similar to C/C++'s `atoi` function).

The algorithm for `myAtoi(string s)` is as follows:

1. Read in and ignore any leading whitespace.
2. Check if the next character (if not already at the end of the string) is `'-'` or `'+'`. Read this character in if it is either. This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.
3. Read in next the characters until the next non-digit character or the end of the input is reached. The rest of the string is ignored.
4. Convert these digits into an integer (i.e. `"123" -> 123`, `"0032" -> 32`). If no digits were read, then the integer is 0. Change the sign as necessary (from step 2).
5. If the integer is out of the 32-bit signed integer range [`-(2^31)`, `(2^31) - 1`], then clamp the integer so that it remains in the range. Specifically, integers less than `-(2^31)` should be clamped to `-(2^31)`, and integers greater than `(2^31) - 1` should be clamped to `(2^31) - 1`.
6. Return the integer as the final result.

**Note**

- Only the space character `' '` is considered a whitespace character.
- **Do not ignore** any characters other than the leading whitespace or the rest of the string after the digits.

**Example 1**

```
Input: s = "42"
Output: 42
Explanation: The underlined characters are what is read in, the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
           ^
The parsed integer is 42.
Since 42 is in the range [-231, 231 - 1], the final result is 42.
```

**Example 2**

```
Input: s = "   -42"
Output: -42
Explanation:
Step 1: "   -42" (leading whitespace is read and ignored)
            ^
Step 2: "   -42" ('-' is read, so the result should be negative)
             ^
Step 3: "   -42" ("42" is read in)
               ^
The parsed integer is -42.
Since -42 is in the range [-231, 231 - 1], the final result is -42.
```

**Example 3**

```
Input: s = "4193 with words"
Output: 4193
Explanation:
Step 1: "4193 with words" (no characters read because there is no leading whitespace)
         ^
Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "4193 with words" ("4193" is read in; reading stops because the next character is a non-digit)
             ^
The parsed integer is 4193.
Since 4193 is in the range [-231, 231 - 1], the final result is 4193.
```

**Constraints**

- `0 <= s.length <= 200`
- `s` consists of English letters (lower-case and upper-case), digits (`0-9`), `' '`, `'+'`, `'-'`, and `'.'`.

## Solution

Below is my working solution for the problem in Leetcode. The main function being called is `myAtoi(String s)`, while `charToInt()` serves as a helper function:

```
class Solution {
    public int myAtoi(String s) {
        if(s.length() == 0){
            return 0;
        }
        int tracker = 0;
        int value = 0;
        int mathMax = (int)Math.pow(2, 31) - 1;
        int mathMin = (-1) * (int)Math.pow(2, 31);
        int multiplier = 1;
        while(s.charAt(tracker) == ' '){
            tracker++;
            if(tracker >= s.length()){
                return value;
            }
        }
        if(s.charAt(tracker) == '-'){
            multiplier = -1;
            tracker++;
        } else if (s.charAt(tracker) == '+'){
            tracker++;
        }
        while(tracker < s.length() && s.charAt(tracker) == '0'){
            tracker++;
            if(tracker >= s.length()){
                return value;
            }
        }
        Map<Character, Integer> map = charToInt();
        int firstInt = -1;
        int prevVal = value;
        String viableString = "";
        while(tracker < s.length() && map.getOrDefault(s.charAt(tracker), -1) != -1){
            int val = map.get(s.charAt(tracker));
            if(firstInt == -1){
                firstInt = val;
            }
            
            value = (value * 10) + val;
            viableString = value + "";
            if(viableString.charAt(0) == '-' || value - (prevVal*10) != val){
                if(multiplier < 0){
                    return mathMin-1;
                }
                return mathMax+1;
            } else if (viableString.length() > 1 && prevVal != Integer.parseInt(viableString.substring(0, viableString.length()-1))){
                if(multiplier < 0){
                    return mathMin-1;
                }
                return mathMax+1;
            }
            prevVal = value;
            tracker++;
        }
        if(value == 0){
            return value;
        }
        value *= multiplier;
        if(value < 0 && multiplier > 0){
            return mathMax+1;
        }
        if(value > 0 && multiplier < 0){
            return mathMin-1;
        }
        return value;
    }
    
    public Map<Character, Integer> charToInt(){
        Map<Character, Integer> result = new HashMap<>();
        result.put('0', 0);
        result.put('1', 1);
        result.put('2', 2);
        result.put('3', 3);
        result.put('4', 4);
        result.put('5', 5);
        result.put('6', 6);
        result.put('7', 7);
        result.put('8', 8);
        result.put('9', 9);
        return result;
    }
}
```
This solution has a runtime of approximately 10-20ms and a memory usage of approximately 39-41MB. 
