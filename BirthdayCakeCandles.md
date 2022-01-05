# Staircase Solution

This problem is available on HackerRank, and can be found through the following link: https://www.hackerrank.com/challenges/birthday-cake-candles/problem

## Problem Description

The description of the "Birthday Cake Candles" problem is as follows:

*You are in charge of the cake for a child's birthday. You have decided the cake will have one candle for each year of their total age. They will only be able to blow out the tallest of the candles. Count how many candles are tallest.*

**Example**

*candles = [4, 4, 1, 3]*

*The maximum height candles are 4 units high. There are 2 of them, so return 2.*

**Function Description**

*Complete the function birthdayCakeCandles in the editor below.*

*birthdayCakeCandles has the following parameter(s):*
- int candles[n]: the candle heights

**Returns**

- *int: the number of candles that are tallest*

**Input Format**

*The first line contains a single integer, n, the size of candles[].
The second line contains n space-separated integers, where each integer i describes the height of candles[i].*

**Constraints**

- *1 <= n <= 10^5*
- *1 <= candles[i] <= 10^7*

**Sample Input 0**

```
4
3 2 1 3
```

**Sample Output 0**

```
2
```

**Explanation**

*Candle heights are [3, 2, 1, 3]. The tallest candles are 3 units, and there are 2 of them.*

## Solution

Below is my working solution for the problem in HackerRank:

```
public static int birthdayCakeCandles(List<Integer> candles) {
    // Write your code here
    if(candles.size() == 1){
        return 1;
    }
    int numOfCandles = 0;
    int maxHeight = -1;
    for(int i = 0; i < candles.size(); i++){
        int candleHeight = candles.get(i);
        if(candleHeight == maxHeight){
            numOfCandles++;
        } else if(candleHeight > maxHeight){
            maxHeight = candleHeight;
            numOfCandles = 1;
        }
    }
    return numOfCandles;
}
```

This solution works against all 9 test cases provided in HackerRank.
