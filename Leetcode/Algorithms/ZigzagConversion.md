# Zigzag Conversion Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/zigzag-conversion/

## Problem Description

The description of the "Zigzag Conversion" problem is as follows:

*The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)*

```
P   A   H   N
A P L S I I G
Y   I   R
```

*And then read line by line: `"PAHNAPLSIIGYIR"`*

*Write the code that will take a string and make this conversion given a number of rows:*

```
string convert(string s, int numRows);
```

**Example 1**

- **Input:** `s = "PAYPALISHIRING"`, `numRows = 3`
- **Output:** `"PAHNAPLSIIGYIR"`


**Example 2**

- **Input:** `s = "PAYPALISHIRING"`, `numRows = 4`
- **Output:** `"PINALSIGYAHRPI"`
- **Explanation:**
```
P     I    N
A   L S  I G
Y A   H R
P     I
```

**Example 3**

- **Input:** `s = "A"`, `numRows = 1`
- **Output:** `"A"`

**Constraints**

- `1 <= s.length <= 1000`
- `s` *consists of English letters (lower-case and upper-case),* `','` *and* `'.'`.
- `1 <= numRows <= 1000`

## Solution

Below is my working solution for the problem in Leetcode:

```
public String convert(String s, int numRows) {
    if(s.length() == 1 || numRows == 1 || numRows == s.length()){
        return s;
    }
    int[] rowNum = new int[s.length()];
    int row = 1;
    boolean ascending = true;
    for(int i = 0; i < s.length(); i++){
        rowNum[i] = row;
        if(row == numRows){
            ascending = false;
        } else if(row - 1 == 0){
            ascending = true;
        }
        if(ascending){
            row++;
        } else {
            row--;
        }
    }
    String updatedString = "";
    row = 1;
    while(row <= numRows){
        for(int m = 0; m < s.length(); m++){
            if(rowNum[m] == row){
                updatedString += s.charAt(m);
            }
        }
        row++;
    }
    return updatedString;
}
```
This solution has a runtime of approximately 80-120ms and a memory usage of approximately 53-54MB. 
