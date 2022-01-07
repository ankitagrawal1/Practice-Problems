# Encryption Solution

This problem is available on HackerRank, and can be found through the following link: https://www.hackerrank.com/challenges/encryption/problem

## Problem Description

*The description of the "Encryption" problem is as follows:*

An English text needs to be encrypted using the following encryption scheme.

First, the spaces are removed from the text. Let *L* be the length of this text.

Then, characters are written into a grid, whose rows and columns have the following constraints:

*floor(sqrt(L)) <= row <= column <= ceil(sqrt(L))*, where *floor(X)* is floor function and *ceil(X)* is ceil function

**Example**

*s = if man was meant to stay on the ground god would have given us roots*

After removing spaces, the string is `54` characters long. *sqrt(54)* is between `7` and `8`, so it is written in the form of a grid with 7 rows and 8 columns.

```
ifmanwas  
meanttos          
tayonthe  
groundgo  
dwouldha  
vegivenu  
sroots
```
- Ensure that *rows x columns >= L*
- If multiple grids satisfy the above conditions, choose the one with the minimum area, i.e., *rows x columns*.

The encoded message is obtained by displaying the characters of each column, with a space between column texts. The encoded message for the grid above is:

`imtgdvs fearwer mayoogo anouuio ntnnlvt wttddes aohghn sseoau`

Create a function to encode a message.

**Function Description**

Complete the encryption function in the editor below.

encryption has the following parameter(s):
- string s: a string to encrypt

**Returns**

- string: the encrypted string

**Input Format**

One line of text, the string *s*

**Constraints**

- *1 <= length of s <= 81*
- *s* contians characters in the range ascii[a-z] and space, ascii(32)

**Sample Input**

```
haveaniceday
```

**Sample Output 0**

```
hae and via ecy
```

**Explanation 0**

*L = 12, sqrt(12)* is between `3` and `4`.

Rewritten with `3` rows and `4` columns:

```
have
anic
eday
```

**Sample Input 1**

```
feedthedog
```

**Sample Output 1**

```
fto ehg ee dd
```

**Explanation 1**

*L = 10, sqrt(10)* is between `3` and `4`.

Rewritten with `3` rows and `4` columns:

```
feed
thed
og
```

**Sample Input 2**

```
chillout
```

**Sample Output 2**

```
clu hlt io
```

**Explanation 2**

*L = 8, sqrt(8)* is between `2` and `3`.

Rewritten with `3` columns and `3` rows (*2 x 3 = 6 < 8* so we have to use `3X3`.)

```
chi
llo
ut
```

## Solution

Below is my working solution for the problem in HackerRank:

```
public static String encryption(String s) {
// Write your code here
    int stringLength = s.length();
    int floor = (int)(Math.sqrt(stringLength));
    int ceil = floor;
    if(floor * ceil != stringLength){
        ceil++;
        if(floor * ceil < stringLength){
            floor++;
        }
    }
    String[][] format = new String[floor][ceil];
    int tracker = 0;
    boolean finished = false;
    for(int i = 0; i < floor; i++){
        for(int k = 0; k < ceil; k++){
            if(tracker >= stringLength){
                finished = true;
                break;
            }
            format[i][k] = s.charAt(tracker) + "";
            tracker++;
        }
        if(finished){
            break;
        }
    }
    tracker = 0;
    int col = 0;
    int row = 0;
    String encrypt = "";
    while(tracker < stringLength){
        if(format[row][col] != null){
            encrypt += format[row][col];
            tracker++;
        }
        row++;
        if(row >= floor){
            row = 0;
            col++;
            encrypt += " ";
        }
    }
    return encrypt;
}
```

This solution works against all 13 test cases provided in HackerRank.
