# Valid Parentheses Solution

This problem is available on LeetCode, and can be found through the following link: https://leetcode.com/problems/valid-parentheses/

## Problem Description

The description of the "Valid Parentheses" problem is as follows:

**Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid. An input string is valid if:**

*Open brackets must be closed by the same type of brackets.*
*Open brackets must be closed in the correct order.*

**Example 1:**

```
Input: s = "()"
Output: true
```

**Example 2:**

```
Input: s = "()[]{}"
Output: true
```

**Example 3:**

```
Input: s = "(]"
Output: false
```

**Example 4:**

```
Input: s = "([)]"
Output: false
```

**Example 5:**

```
Input: s = "{[]}"
Output: true
```

**Constraints:**

*1 <= s.length <= 104*

*s consists of parentheses only '()[]{}'.*

## Solution

The format of this problem lent itself well to the use of a stack--in particular, I could use a Stack to store characters from the string so long as they were open-bracket characters. Then, once a closed-bracket character is found, I could get the most recent open-bracket character from the stack to determine if the type of bracket matches or if there are any errors that would require me to return false. If I get through the entire substring without any errors in the stack and with an empty stack at the end, that would signify that I had been given a valid set of parentheses.

### Initial Solution

The following solution successfully passed LeetCode's submission system:

```
class Solution {
    public boolean isValid(String s) {
        if(s.length() == 0){
            return true;
        }
        else if(s.length() == 1){
            return false;
        }
        Stack<Character> letters = new Stack<>();
        letters.push(s.charAt(0));
        for(int i = 1; i < s.length(); i++){
            char nextChar = s.charAt(i);
            if(nextChar == '}' || nextChar == ']' || nextChar == ')'){
                if(letters.isEmpty()){
                    return false;
                }
                else{
                    char previous = letters.pop();
                    if ((nextChar == '}' && previous != '{') ||
                        (nextChar == ']' && previous != '[') ||
                        (nextChar == ')' && previous != '(')){
                        return false;
                    }
                }
            }
            else{
                letters.push(nextChar);
            }
        }
        if(!letters.isEmpty()){
            return false;
        }
        return true;
    }
}
```
According to LeetCode, the solution had a runtime of 2 ms and was faster than 27.13% of Java online submissions for the problem at the time.

### Improvement: Base Cases

Upon examining the solution, I noticed that the base cases weren't really necessary. Since the constraints of the problem specified that I would also be given a string with at least one character, checking for a string with no characters was not needed. For a string with only one character, the general algorithm still worked for that case because we would be left with a non-empty stack and therefore return false. I could therefore remove both base case checks from the start of the algorithm and still achieve a successful solution.

### Improved Solution

The following solution also passed LeetCode's submission system, and removes both base case checks seen in the "Initial Solution" version:

```
class Solution {
    public boolean isValid(String s) {
        Stack<Character> letters = new Stack<>();
        letters.push(s.charAt(0));
        for(int i = 1; i < s.length(); i++){
            char nextChar = s.charAt(i);
            if(nextChar == '}' || nextChar == ']' || nextChar == ')'){
                if(letters.isEmpty()){
                    return false;
                }
                else{
                    char previous = letters.pop();
                    if ((nextChar == '}' && previous != '{') ||
                        (nextChar == ']' && previous != '[') ||
                        (nextChar == ')' && previous != '(')){
                        return false;
                    }
                }
            }
            else{
                letters.push(nextChar);
            }
        }
        if(!letters.isEmpty()){
            return false;
        }
        return true;
    }
}
```
According to LeetCode, the solution had a runtime of 1 ms and was faster than 98.74% of Java online submissions for the problem at the time.
