# [Medium 6. ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/submissions/)

## Problem:
Input: s = "PAYPALISHIRING", numRows = 4  
Output: "PINALSIGYAHRPI"  
Explanation:  
<pre>
P     I    N
A   L S  I G
Y A   H R
P     I
</pre>

## Thought:

+ seperate "v" shape substr, each substr size(distance) is 2*(numsRow-1).
+ for the first n chars, add to result.
+ for the rest in each line, the pattern is that:
  * for odd addiction, the distance from previous one is substr_size - 2*(numsRow-1).
  * for even addiction, the distance from previous one is 2*(numRows-1).
  * check for boundary
  
## Code:

```c++
class Solution {
public:
    string convert(string s, int numRows) {
        if(s.length() <= numRows) return s;
        if(numRows <= 1) return s;
        
        string res = "";
        int row = numRows;
        int distance = 2*(numRows-1);
        for(int i = 0; i < numRows; i++){
            int count = i;
            
            if(i == 0 || i == numRows-1){
                while(count < s.length()){
                    res += s[count];
                    count += distance;
                }
            } else {
                //odd  +(distance-2*i)
                //even  +(2*i)
                bool odd_flag = true;
                while(count < s.length()){
                    if(odd_flag){
                        res += s[count];
                        count += ((distance)-2*i);
                        odd_flag = false;
                    } else {
                        res += s[count];
                        count += (2*i);
                        odd_flag = true;
                    }
                }
            }
        }
        return res;
    }
};
```

## Result:

Runtime: 24 ms, faster than 95.72% of C++ online submissions for ZigZag Conversion.  
Memory Usage: 16.9 MB, less than 64.88% of C++ online submissions for ZigZag Conversion.  
