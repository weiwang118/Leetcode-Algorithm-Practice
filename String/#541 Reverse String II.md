#### #541 Reverse String II
[Leetcode #541](https://leetcode.com/problems/reverse-string-ii/)  

##### My Solution
```
class Solution {
public:
    string reverseStr(string s, int k) {
        if(s.length()<k)
                reverse(s.begin(),s.end());
        else{
                for(int i=0;i<s.length();i=i+2*k){
                        if(i+k>s.length())
                        reverse(s.begin()+i,s.end());
                        else reverse(s.begin()+i,s.begin()+i+k);
                }
        }
            return s;
    }
};
```
