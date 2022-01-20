#### #387 First Unique Character in a String
[Leetcode #387](https://leetcode.com/problems/first-unique-character-in-a-string/)  

##### My Solution
```
class Solution {
public:
    int firstUniqChar(string s) {
        int hash[26]={0};
        for(int i=0;i<s.length();i++)
                hash[s[i]-'a']++;
        for(int i=0;i<s.length();i++)
        {
                if(hash[s[i]-'a']==1) return i;
        }
            return -1;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
