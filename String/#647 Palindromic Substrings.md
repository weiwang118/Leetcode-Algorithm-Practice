#### #647 Palindromic Substrings
[Leetcode #647](https://leetcode.com/problems/palindromic-substrings/)  

##### My Solution
```
class Solution {
public:
    int count=0;
    void sub(string &s,int start, int end){
         while(start>=0 && end<s.size()&&s[start]==s[end]){
                 start--;
                 end++;
                 count++;
         }
    }
    int countSubstrings(string s) {
        for(int i=0;i<s.length();i++){
                sub(s,i,i);
                sub(s,i,i+1);
        }
            return count;
    }
};
```
