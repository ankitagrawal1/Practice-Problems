# Word Search Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/word-search/

## Problem Description

*The description of the "Word Search" problem is as follows:*

Given an `m x n` grid of characters `board` and a string `word`, return `true` *if* `word` *exists in the grid*.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

*Note: The examples below in Leetcode also include a visual representation. Please use the link referenced above to view the problem in Leetcode and find the accompanying images for the three examples.*

**Example 1:**

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

**Example 2:**

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```

**Example 3:**
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```

**Constraints**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` and `word` consists of only lowercase and uppercase English letters.

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

## Solution

Below is my working solution for the problem in Leetcode. The main function being called is `exist(char[][] board, String word)`, while `checkWord(char[][] board, String word, String currentWord, int[][] visited, int x, int y, int nextChar)` serves as a helper function:

```
class Solution {
    public boolean exist(char[][] board, String word) {
        boolean result = false;
        for(int i = 0; i < board.length; i++){
            for(int m = 0; m < board[0].length; m++){
                if(board[i][m] == word.charAt(0)){
                    int[][] visitedBoard = new int[board.length][board[0].length];
                    visitedBoard[i][m] = 1;
                    result = checkWord(board, word, board[i][m]+"", visitedBoard, i, m, 1);
                }
                if(result){
                    return result;
                }
            }
        }
        return false;
    }
    
    public boolean checkWord(char[][] board, String word, String currentWord, int[][] visited, int x, int y, int nextChar){
        if(currentWord.equals(word)){
            return true;
        }
        boolean result = false;
        if(x - 1 >= 0){
            if(visited[x-1][y] != 1 && board[x-1][y] == word.charAt(nextChar)){
                visited[x-1][y] = 1;
                result = checkWord(board, word, currentWord + board[x-1][y], visited, x-1, y, nextChar+1);
                if(result){
                    return result;
                }
                visited[x-1][y] = 0;
            }
        }
        if(y + 1 < board[0].length){
            if(visited[x][y+1] != 1 && board[x][y+1] == word.charAt(nextChar)){
                visited[x][y+1] = 1;
                result = checkWord(board, word, currentWord + board[x][y+1], visited, x, y+1, nextChar+1);
                if(result){
                    return result;
                }
                visited[x][y+1] = 0;
            }
        }
        if(x + 1 < board.length){
            if(visited[x+1][y] != 1 && board[x+1][y] == word.charAt(nextChar)){
                visited[x+1][y] = 1;
                result = checkWord(board, word, currentWord + board[x+1][y], visited, x+1, y, nextChar+1);
                if(result){
                    return result;
                }
                visited[x+1][y] = 0;
            }
        }
        if(y - 1 >= 0){
            if(visited[x][y-1] != 1 && board[x][y-1] == word.charAt(nextChar)){
                visited[x][y-1] = 1;
                result = checkWord(board, word, currentWord + board[x][y-1], visited, x, y-1, nextChar+1);
                if(result){
                    return result;
                }
                visited[x][y-1] = 0;
            }
        }
        
        return result;
    }
}
```
This solution has a runtime of approximately 800-1300ms and a memory usage of approximately 118-119MB. 
