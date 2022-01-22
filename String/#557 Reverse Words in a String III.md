#### #557 Reverse Words in a String III
[Leetcode #557](https://leetcode.com/problems/reverse-words-in-a-string-iii/)  

##### My Solution
```
class Solution {
public:
    string reverseWords(string s) {
        s+=' ';
        string temp="";
        string res;
        for(char ch:s){
                if(ch==' '){
                        reverse(temp.begin(),temp.end());
                        res+=temp;
                        res+=ch;
                        temp.clear();
                }
                else
                        temp+=ch;
                
        }
            res.resize(res.size()-1);
            return res;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  
