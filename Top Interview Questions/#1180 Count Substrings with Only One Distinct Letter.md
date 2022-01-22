#### #1180 Count Substrings with Only One Distinct Letter
[Leetcode #1180](https://leetcode.com/problems/count-substrings-with-only-one-distinct-letter/)  

##### My Solution
```
class Solution {
public:
    int countLetters(string s) {
        int count=1;
        int sum=1;
        for(int i=1;i<s.size();i++){
                if(s[i]==s[i-1])
                    count++;
                else
                     count=1;
                sum+=count;
        }
            return sum;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
