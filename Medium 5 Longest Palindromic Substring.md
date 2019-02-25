# [Medium 5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

## Problem:

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.  

Example 1:  
  
Input: "babad"  
Output: "bab"  
Note: "aba" is also a valid answer.  

## Thoughts:
+ First Approach:
+ iterate the string
+ for each occurence j of the item i:  
+ determine the s.substr(i to j) is palindrome;  

**isPalindrome is O(n), iteration takes O(n^2) in worst case;**

- Second:
- For odd palindrome: iterate string;
- for each char, expand it from the center, stop when s[i]!=s[j];
- compare substr from i to j with result;
- For even palindrome: repeat previous action, but this time j = i+1;

**this takes O(n^2)**

* [expand around center]()

## Code:
```c++
class Solution {
public:
    string longestPalindrome(string s) {
        string res = "";
        
        for(int c = 0; c < s.length(); c++){
            size_t next = s.find(s[c], 0);
            while(next != string::npos){
                string temp = s.substr(c, next-c+1);
                if(isPalindrome(temp) && temp.length()>res.length()){
                    res = temp;
                }
                next = s.find(s[c], next+1);
            }
        }
        
        if(res.empty()){
            return res+s.front();
        }
        return res;
    }
    
    bool isPalindrome(string s){
        if(s.length() > 1){
            string::iterator left, right;
            for(left=s.begin(), right=s.end()-1; left<right; ++left, --right){
                if(*left != *right){
                    return false;
                }
            }
            return true;
        } else {
            return true;
        }
    }
};
```
```c++
class Solution {
public:
    string longestPalindrome(string s) {
        string result="";
        if(s.size() == 0)
            return result;
        //for odd length
        for(int i=0; i<=s.size()-1; i++){
            int j=i, k=i;
            string tmp = "";
            while( j>=0 && k<= s.size()-1 && s[j] == s[k] ){
                j--;
                k++;
            }
            if(j!=k)
                tmp = s.substr(j+1, k-j-1);
            else
                tmp+=s[i];
            if(tmp.size() >= result.size())
                result = tmp;
        }
        //for even length
        for(int i=0, j=1; j<=s.size()-1; i++, j++){
            int m=i, n=j;
            string tmp = "";
            while( m>=0 && n<= s.size()-1 && s[m] == s[n] ){
                m--;
                n++;
            }
            if(n-m !=1)
                tmp = s.substr(m+1, n-m-1);

            if(tmp.size() >= result.size())
                result = tmp;
        }
        
        return result;
    }
};
```
