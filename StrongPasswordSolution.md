# Strong Password Solution

This problem is available on HackerRank, and can be found through the following link: https://www.hackerrank.com/challenges/strong-password/problem

## Problem Description

The description of the "Strong Password" problem is as follows:

**Louise joined a social networking site to stay in touch with her friends. The signup page required her to input a name and a password. However, the password must be strong. The website considers a password to be strong if it satisfies the following criteria:**

*Its length is at least 6.*

*It contains at least one digit.*

*It contains at least one lowercase English character.*

*It contains at least one uppercase English character.*

*It contains at least one special character. The special characters are: !@#$%^&*()-+*

**She typed a random string of length in the password field but wasn't sure if it was strong. Given the string she typed, can you find the minimum number of characters she must add to make her password strong?**

*Note: Here's the set of types of characters in a form you can paste in your solution:*

```
numbers = "0123456789"
lower_case = "abcdefghijklmnopqrstuvwxyz"
upper_case = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
special_characters = "!@#$%^&*()-+"
```

**Input Format**

*The first line contains an integer n denoting the length of the string.*

*The second line contains a string consisting of n characters, the password typed by Louise. Each character is either a lowercase/uppercase English alphabet, a digit, or a special character.*

**Constraints**

*Output Format*

*Print a single line containing a single integer denoting the answer to the problem.*

**Sample Input 0**

```
3
Ab1
```

**Sample Output 0**

```
3
```

**Explanation 0**

*She can make the password strong by adding  characters, for example, $hk, turning the password into Ab1$hk which is strong. 2 characters aren't enough since the length must be at least 6.*

**Sample Input 1**

```
11
#HackerRank
```

**Sample Output 1**

```
1
```

**Explanation 1**

*The password isn't strong, but she can make it strong by adding a single digit.*

## Solution

For this question, I thought I would follow what HackerRank suggested with the strings it gave for each type of character required in the password. Given such strings, it seemed simplest to loop through each string for each character of the password, checking if any of the type conditions are met until the end of the string is reached.

### Initial Solution

I initially considered storing all the given strings into an ArrayList of strings; however, I realized that this could make it slightly more difficult to determine if a condition is met when a character is found in any string in the ArrayList. Therefore, as a quick solution, I opted to first check the length of the password to see if any characters would have to be required, regardless of if the character type checks are met. I then loop through each character in the password, and for each character, I loop through each of the four given strings to determine if a particular character type is found. If found, the proper associated variable is set, and once all loops are completed, we are left with what characters still need to be added. I could then compare the number of character types that need to be added with the number of characters needed to reach the minimum password length, and I'd return the greater of the two.

The following solution successfully passed HackerRank's submission system, which had 89 test cases:

```
// Complete the minimumNumber function below.
    static int minimumNumber(int n, String password) {
        // Return the minimum number of characters to make the password strong
        String numbers = "0123456789";
        String lower_case = "abcdefghijklmnopqrstuvwxyz";
        String upper_case = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String special_characters = "!@#$%^&*()-+";

        int add = 0;
        if(n < 6){
            add = 6 - n;
        }
        int lowerCase = 1;
        int num = 1;
        int upperCase = 1;
        int specialCharacter = 1;

        for(int i = 0; i < password.length(); i++){
            if(num == 1){
                for(int k = 0; k < numbers.length(); k++){
                    if(password.charAt(i) == numbers.charAt(k) && num == 1){
                        num--;
                    }
                }
            }
            if(lowerCase == 1){
                for(int l = 0; l < lower_case.length(); l++){
                    if(password.charAt(i) == lower_case.charAt(l) && lowerCase == 1){
                        lowerCase--;
                    }
                }
            }
            if(upperCase == 1){
                for(int m = 0; m < upper_case.length(); m++){
                    if(password.charAt(i) == upper_case.charAt(m) && upperCase == 1){
                        upperCase--;
                    }
                }
            }
                if(specialCharacter == 1){
                for(int o = 0; o < special_characters.length(); o++){
                    if(password.charAt(i) == special_characters.charAt(o) && specialCharacter == 1){
                        specialCharacter--;
                    }
                }
            }
        }
        
        int necessaryChar = lowerCase+upperCase+specialCharacter+num;
        if(add >= necessaryChar){
            return add;
        }
        else{
            return necessaryChar;
        }

    }
```

### Improvements

There are multiple improvements that could be made with the algorithm. To begin, while the set of strings given in the initial question are helpful, searching through each string for every character feels fairly ineffective and time-inefficient. Therefore, altering the search techniques would be the best way to optimize the solution. For example, rather than looping through the string of numbers in ```numbers```, the isDigit() function could be applied to the individual characters in ```password``` instead. Similarly, using isLowerCase() and isUpperCase() functions could improve the time efficiency of the algorithm by eliminating other loops. Such an implementation would also eliminate the reduant if-statements checking for whether or not particular variables equal 1 or 0.

Secondly, changing the repeated if-statements to ```if-else``` statements would improve efficiency [e.g., we would not be checking for lowercase characters if a lowercase character was already found, we would not be checking a character to be uppercase if it was already decided as lowercase, etc.].

Lastly, when comparing ```necessaryChar``` and ```add``` at the end of the solution, the ```max()``` function from the Math library could be called to return the greater value rather than explicitly using an ```if-else``` statement.

### Improved Solution

Utilizing these guidelines, the following solution is an improved version of the initial solution and successfully passed HackerRank's submission system:

```
// Complete the minimumNumber function below.
    static int minimumNumber(int n, String password) {
        // Return the minimum number of characters to make the password strong
        String special_characters = "!@#$%^&*()-+";

        int add = 0;
        if(n < 6){
            add = 6 - n;
        }
        int lowerCase = 1;
        int num = 1;
        int upperCase = 1;
        int specialCharacter = 1;

        for(int i = 0; i < password.length(); i++){
            if(num == 1 && Character.isDigit(password.charAt(i))){
                num--;
            }
            else if(lowerCase == 1 && Character.isLowerCase(password.charAt(i))){
                lowerCase--;
            }
            else if(upperCase == 1 && Character.isUpperCase(password.charAt(i))){
                upperCase--;
            }
            else if(specialCharacter == 1){
                for(int o = 0; o < special_characters.length(); o++){
                    if(password.charAt(i) == special_characters.charAt(o) && specialCharacter == 1){
                        specialCharacter--;
                    }
                }
            }
        }
        
        return Math.max(lowerCase+upperCase+specialCharacter+num, add);

    }
```
