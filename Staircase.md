# Staircase Solution

This problem is available on HackerRank, and can be found through the following link: https://www.hackerrank.com/challenges/staircase/problem

## Problem Description

The description of the "Staircase" problem is as follows:

*This is a staircase of size n = 4:*
```
   #
  ##
 ###
####
```
*Its base and height are both equal to n. It is drawn using # symbols and spaces. The last line is not preceded by any spaces.
Write a program that prints a staircase of size n.*

**Function Description**

*Complete the staircase function in the editor below.*
*staircase has the following parameter(s):*
- int n: an integer

**Print**

*Print a staircase as described above.*

**Input Format**

*A single integer, n, denoting the size of the staircase.*

**Constraints**

*0 < n <= 100*

**Output Format**

*Print a staircase of size n using # symbols and spaces.*

***Note:*** *The last line must have 0 spaces in it.*

**Sample Input**

```
6
```

**Sample Output**

```
     #
    ##
   ###
  ####
 #####
######
```

**Explanation**

*The staircase is right-aligned, composed of # symbols and spaces, and has a height and width of n = 6.*

## Solution

Below is my working solution for the problem in HackerRank:

```
    public static void staircase(int n) {
    if(n == 0){
        return;
    }
    String stair = "#";
    for(int i = 2; i <= n; i++){
        stair = " " + stair + "#";
    }
    for(int i = 0; i < n; i++){
        System.out.println(stair.substring(0, n));
        stair = stair.substring(1);
    }
    }
```

This solution works against all 9 test cases provided in HackerRank.
