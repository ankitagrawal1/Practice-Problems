# Divisible Sum Pairs Solution

This problem is available on HackerRank, and can be found through the following link: https://www.hackerrank.com/challenges/divisible-sum-pairs/problem

## Problem Description

*The description of the "Divisible Sum Pairs" problem is as follows:*

Given an array of integers and a positive integer `k`, determine the number of `(i,j)` pairs where `i<j` and `ar[i]` + `ar[j]` is divisible by `k`.

**Example**

`ar = [1, 2, 3, 4, 5, 6]`

`k = 5`

Three pairs meet the criteria: `[1, 4]`, `[2, 3]`, and `[4, 6]`.

**Function Description**

Complete the divisibleSumPairs function in the editor below.

divisibleSumPairs has the following parameter(s):

- int n: the length of array `ar`
- int ar[n]: an array of integers
- int k: the integer divisor

**Returns**

- int: the number of pairs

**Input Format**

The first line contains 2 space-separated integers, `n` and `k`.
The second line contains `n` space-separated integers, each a value of `arr[i]`.

**Constraints**

- *2 <= n <= 100*
- *1 <= k <= 100*
- *1 <= ar[i] <= 100*

**Sample Input**

```
STDIN           Function
-----           --------
6 3             n = 6, k = 3
1 3 2 6 1 2     ar = [1, 3, 2, 6, 1, 2]
```

**Sample Output**

```
5
```

**Explanation**

Here are the 5 valid pairs when `k = 3`:
- `(0, 2) --> ar[0] + ar[2] = 1 + 2 = 3`
- `(0, 5) --> ar[0] + ar[5] = 1 + 2 = 3`
- `(1, 3) --> ar[1] + ar[3] = 3 + 6 = 9`
- `(2, 4) --> ar[2] + ar[4] = 2 + 1 = 3`
- `(4, 5) --> ar[4] + ar[5] = 1 + 2 = 3`

## Solution

Below is my working solution for the problem in HackerRank:

```
public static int divisibleSumPairs(int n, int k, List<Integer> ar) {
    // Write your code here
    int numOfPairs = 0;
    for(int i = 0; i < ar.size(); i++){
        for(int m = i+1; m < ar.size(); m++){
            if((ar.get(i) + ar.get(m))%k == 0){
                numOfPairs++;
            }
        }
    }
    return numOfPairs;
}
```

This solution works against all 20 test cases provided in HackerRank.
