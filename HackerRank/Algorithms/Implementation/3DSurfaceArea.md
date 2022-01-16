# 3D Surface Area Solution

This problem is available on HackerRank, and can be found through the following link: https://www.hackerrank.com/challenges/3d-surface-area/problem

## Problem Description

*The description of the "3D Surface Area" problem is as follows:*

Madison, is a little girl who is fond of toys. Her friend Mason works in a toy manufacturing factory. Mason has a 2D board *A* of size *H x W* with *H* rows and *W* columns. The board is divided into cells of size `1 x 1` with each cell indicated by its coordinate `(i, j)`. The cell  has an integer `A_(i,j)` written on it. To create the toy, Mason stacks `A_(i,j)` number of cubes of size `1 x 1 x 1` on the cell `(i, j)`.

Given the description of the board showing the values of `A_(i,j)` and that the price of the toy is equal to the 3d surface area find the price of the toy.

*Note: The problem statement in HackerRank includes a visual depiction of the Sample Input 1 described further below. Please use the link provided above to find the visual in HackerRank.*

**Input Format**

The first line contains two space-separated integers *H* and *W* the height and the width of the board respectively.

The next *H* lines contains *W* space separated integers. The *jth* integer in *ith* line denotes `A_(i,j)`.

**Constraints**

- *1 <= H, W <= 100*
- *1 <= A_(i,j) <= 100*

**Output Format**

Print the required answer, i.e the price of the toy, in one line.

**Sample Input 0**

```
1 1
1
```

**Sample Output 0**

```
6
```

**Explanation 0**

*Note: the explanation in HackerRank includes a visual diagram of the cube. Please use the link included at the top of this document to find the visual in HackerRank.*

The surface area of `1 x 1 x 1` cube is 6.

**Sample Input 1**

```
3 3
1 3 4
2 2 3
1 2 4
```

**Sample Output 1**

```
60
```

**Explanation 1**

The sample input corresponds to the figure described in problem statement.

## Solution

It took me a bit of time to first determine how I should be going about calculating the surface area for the possible toys. However, after briefly examining sample input 1 with a friend to try and confirm its surface area, I realized I was overcomplicating the problem -- as a result, I rethought how I was calculating the surface area manually and translated that solution successfully into code. Below is my subsequently working solution for the problem in HackerRank:

```
public static int surfaceArea(List<List<Integer>> A) {
    // Write your code here
    if(A.size() == 1 && A.get(0).size() == 1){
        return 4 * A.get(0).get(0) + 2;
    }
    int area = 0;
    int length = A.size();
    int width = A.get(0).size();
    area += (2 * length * width); //top and bottom view    
    //left view
    for(int i = 0; i < length; i++){
        int surfaceAreaToAdd = A.get(i).get(0);
        int currentHeight = surfaceAreaToAdd;
        for(int k = 1; k < width; k++){
            int height = A.get(i).get(k);
            if(height > currentHeight){
                surfaceAreaToAdd += (height - currentHeight);
            }
            currentHeight = height;
        }
        area += surfaceAreaToAdd;
    }
    
    //front view
    for(int k = 0; k < width; k++){
        int surfaceAreaToAdd = A.get(length-1).get(k);
        int currentHeight = surfaceAreaToAdd;
        for(int i = length-2; i >= 0; i--){
            int height = A.get(i).get(k);
            if(height > currentHeight){
                surfaceAreaToAdd += (height - currentHeight);
            }
            currentHeight = height;
        }
        area += surfaceAreaToAdd;
    }
    
    // right view
    for(int i = length-1; i >= 0; i--){
        int surfaceAreaToAdd = A.get(i).get(width-1);
        int currentHeight = surfaceAreaToAdd;
        for(int k = width-2; k >= 0; k--){
            int height = A.get(i).get(k);
            if(height > currentHeight){
                surfaceAreaToAdd += (height - currentHeight);
            }
            currentHeight = height;
        }
        area += surfaceAreaToAdd;
    }
    
    // back view
    for(int k = width-1; k >= 0; k--){
        int surfaceAreaToAdd = A.get(0).get(k);
        int currentHeight = surfaceAreaToAdd;
        for(int i = 1; i < length; i++){
            int height = A.get(i).get(k);
            if(height > currentHeight){
                surfaceAreaToAdd += (height - currentHeight);
            }
            currentHeight = height;
        }
        area += surfaceAreaToAdd;
    }   
    
    return area;
}
```

This solution works against all 26 test cases provided in HackerRank.
