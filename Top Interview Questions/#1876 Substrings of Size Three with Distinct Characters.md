#### #1876 Substrings of Size Three with Distinct Characters
[Leetcode #1876](https://leetcode.com/problems/substrings-of-size-three-with-distinct-characters/)  

##### My Solution
```
class Solution {
public:
    int countGoodSubstrings(string s) {
        int count=0;
        if(s.size()<3)return 0;
        for(int i=0;i<s.size()-2;i++){
                set<char> set(&s[i],&s[i+3]);
                if(set.size()==3)
                        count++;
                set.clear();
        }
            return count;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(3)  
