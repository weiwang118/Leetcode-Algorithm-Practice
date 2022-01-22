#### 58. Length of Last Word
[Leetcode #58](https://leetcode.com/problems/length-of-last-word/)  

##### My Solution
Approach 1: split the string and return the last  
```
class Solution {
public:
    int lengthOfLastWord(string s) {
        s+=" ";
        string temp="";
        vector<string> res;
        for(char ch:s){
                if(ch==' '){
                        if(!temp.empty())
                                res.push_back(temp);
                        temp.clear();
                }
                else{
                        temp+=ch;
                }
        }
           return res.back().size();
    }
};
```
Time complexity: O(n)  
Space Complexity: O(n)  

Approach 2: Iterate from the end  
```
class Solution {
public:
    int lengthOfLastWord(string s) {
      string temp="";
      for(int i=s.size()-1;i>=0;i--){
              
              if(s[i]==' '&&temp.empty())
                      continue;
              else if(s[i]==' '&&!temp.empty())
                      break;
              else temp+=s[i];
              
      }
            return temp.size();
    }
};
```
Time Complexity: O(n)  
Space Compexity: O(n)  

