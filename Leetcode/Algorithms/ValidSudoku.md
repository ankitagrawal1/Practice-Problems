# Valid Sudoku Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/valid-sudoku/

## Problem Description

*The description of the "Valid Sudoku" problem is as follows:*

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:
- Each row must contain the digits `1-9` without repetition.
- Each column must contain the digits `1-9` without repetition.
- Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

**Example 1:**

*Note: This example in Leetcode also includes a visual representation of the input. Please use the link referenced above to view the problem in Leetcode and find the accompanying image for this example.*

```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

**Example 2:**

```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

**Constraints**

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or `'.'`.


## Solution

Below is my working solution for the problem in Leetcode:

```
class Solution {
    public boolean isValidSudoku(char[][] board) {
        Map<Integer, List<Character>> map = new HashMap<>();
        for(int i = 0; i < 9; i++){
            for(int m = 0; m < 9; m++){
                char value = board[i][m];
                if(value != '.'){
                    List<Character> rowList = map.getOrDefault(i, new ArrayList<Character>());
                    if(rowList.contains(value)){
                        return false;
                    }
                    List<Character> colList = map.getOrDefault(m+9, new ArrayList<Character>());
                    if(colList.contains(value)){
                        return false;
                    }
                    int box = (i/3)*3 + (m/3);
                    List<Character> boxList = map.getOrDefault(18+box, new ArrayList<Character>());
                    if(boxList.contains(value)){
                        return false;
                    }
                    rowList.add(value);
                    map.put(i, rowList);
                    colList.add(value);
                    map.put(m+9, colList);
                    boxList.add(value);
                    map.put(18+box, boxList);    
                }
            }
        }
        
        return true;
        
    }
}
```
This solution has a runtime of approximately 5-10 ms and a memory usage of approximately 46-48MB. 
