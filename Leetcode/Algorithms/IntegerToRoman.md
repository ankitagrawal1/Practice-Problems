# Integer to Roman Solution

This problem is available on Leetcode, and can be found through the following link: https://leetcode.com/problems/integer-to-roman

## Problem Description

The description of the "Integer to Roman" problem is as follows:

*Roman numerals are represented by seven different symbols:* `I`, `V`, `X`, `L`, `C`, `D` *and* `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

*For example,* `2` *is written as* `II` *in Roman numeral, just two one's added together.* `12` *is written as* `XII`*, which is simply* `X + II`*. The number* `27` *is written as* `XXVII`*, which is* `XX + V + II`.

*Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not* `IIII`*. Instead, the number four is written as* `IV`*. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as* `IX`*. There are six instances where subtraction is used:*

- `I` *can be placed before* `V` *(5) and* `X` *(10) to make 4 and 9.*
- `X` *can be placed before* `L` *(50) and* `C` *(100) to make 40 and 90.*
- `C` *can be placed before* `D` *(500) and* `M` *(1000) to make 400 and 900.*

*Given an integer, convert it to a roman numeral.*

**Example 1**

```
Input: num = 3
Output: "III"
Explanation: 3 is represented as 3 ones.
```

**Example 2**

```
Input: num = 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
```

**Example 3**

```
Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

**Constraints**

- `1 <= num <= 3999`

## Solution

Below is my working solution for the problem in Leetcode. The main function being called is `intToRoman()`, while `createIntToRomanMap()`, `createListOfNums()`, and `convertToRoman()` serve as helper functions:

```
class Solution {
    public String intToRoman(int num) {
        Map<Integer, String> intToRoman = createIntToRomanMap();
        List<Integer> numsToTest = createListOfNums();
        return convertToRoman(num, intToRoman, numsToTest, 0, "");
    }
    
    public Map<Integer, String> createIntToRomanMap() {
        Map<Integer, String> intToRoman = new HashMap<>();
        intToRoman.put(1, "I");
        intToRoman.put(4, "IV");
        intToRoman.put(5, "V");
        intToRoman.put(9, "IX");
        intToRoman.put(10, "X");
        intToRoman.put(40, "XL");
        intToRoman.put(50, "L");
        intToRoman.put(90, "XC");
        intToRoman.put(100, "C");
        intToRoman.put(400, "CD");
        intToRoman.put(500, "D");
        intToRoman.put(900, "CM");
        intToRoman.put(1000, "M");
        
        return intToRoman;
    }
    
    public List<Integer> createListOfNums(){
        List<Integer> list = new ArrayList<>();
        list.add(1000);
        list.add(900);
        list.add(500);
        list.add(400);
        list.add(100);
        list.add(90);
        list.add(50);
        list.add(40);
        list.add(10);
        list.add(9);
        list.add(5);
        list.add(4);
        list.add(1);
        
        return list;
    }
    
    public String convertToRoman(int num, Map<Integer, String> map, List<Integer> list, int index, String convert){
        if(num == 0){
            return convert;
        }
        if(!map.getOrDefault(num, "-1").equals("-1")){
            convert += map.get(num);
            return convert;
        }
        while(num/list.get(index) == 0){
            index++;
        }
        int divisor = list.get(index);
        int numOfTimes = num/divisor;
        int remainder = num%divisor;
        String roman = map.get(divisor);
        for(int i = 0; i < numOfTimes; i++){
            convert += roman;
        } 
        num -= (numOfTimes * divisor);
        return convertToRoman(num, map, list, index, convert);
    }
}
```
This solution has a runtime of approximately 10-25ms and a memory usage of approximately 39-47MB. 
