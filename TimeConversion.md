# Time Conversion Solution

This problem is available on HackerRank, and can be found through the following link: https://www.hackerrank.com/challenges/time-conversion/problem

## Problem Description

The description of the "Time Conversion" problem is as follows:

*Given a time in -hour AM/PM format, convert it to military (24-hour) time.*

*Note:*

*- 12:00:00AM on a 12-hour clock is 00:00:00 on a 24-hour clock.*

*- 12:00:00PM on a 12-hour clock is 12:00:00 on a 24-hour clock.*

**Example**
- *s = `12:01:00PM`*

*Return `12:01:00`*
- *s = `12:01:00AM`*

*Return `00:01:00`*

**Function Description**

*Complete the timeConversion function in the editor below. It should return a new string representing the input time in 24 hour format.*

*timeConversion has the following parameter(s):*
- string s: a time in 12 hour format

**Returns**

- string: the time in 24 hour format

**Input Format**

*A single string  that represents a time in 12-hour clock format (i.e.: `hh:mm:ssAM` or `hh:mm:ssPM`).*

**Constraints**

- *All input times are valid*

**Sample Input 0**

```
07:05:45PM
```

**Sample Output 0**

```
19:05:45
```

## Solution

Below is my working solution for the problem in HackerRank:

```
public static String timeConversion(String s) {
// Write your code here
String timeOfDay = s.substring(8);
int hour = Integer.parseInt(s.substring(0,2));
String updatedHour = hour + "";
if(timeOfDay.equals("AM")){
    if(hour != 12){
        return s.substring(0,8);
    }
    hour-=12;
    updatedHour = hour + "0";
}
else{
    if(hour == 12){
        return s.substring(0,8);
    }
    hour+=12;
    updatedHour = hour + ""; 
}
return updatedHour + s.substring(2,8);
}
```

This solution works against all 10 test cases provided in HackerRank.
