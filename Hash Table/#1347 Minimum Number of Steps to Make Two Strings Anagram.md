#### #1347 Minimum Number of Steps to Make Two Strings Anagram
[Leetcode #1347](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/)  

##### My Solution
```
class Solution {
public:
    int minSteps(string s, string t) {
        vector<int> hashtable(26,0);
        int steps=0;
        for(int i=0;i<s.size();i++)
                hashtable[s[i]-'a']++;
        for(int j=0;j<t.size();j++)
                hashtable[t[j]-'a']--;
        for(int i=0;i<26;i++){
                if(hashtable[i]>0)
                        steps+=hashtable[i];
        }
            return steps;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
