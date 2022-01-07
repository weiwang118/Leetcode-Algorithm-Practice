#### #242 Valid Anagram
[Leetcode #242](https://leetcode.com/problems/valid-anagram/)  
##### My Solution
```
class Solution {
public:
    bool isAnagram(string s, string t) {
        int record[26]={0};
        if(s.length()!=t.length())return false;
        for(int i=0;i<s.length();i++){
                record[s[i]%97]++;
                record[t[i]%97]--;
        }
        for(int i=0;i<26;i++){
                if(record[i]!=0)return false;
        }
            return true;
        
    }
};
```
Time Complexity: O(n)  
Space Complexity:O(1)  

##### Solution from Carl
```
class Solution {
public:
    bool isAnagram(string s, string t) {
        int record[26] = {0};
        for (int i = 0; i < s.size(); i++) {
            // 并不需要记住字符a的ASCII，只要求出一个相对数值就可以了
            record[s[i] - 'a']++;
        }
        for (int i = 0; i < t.size(); i++) {
            record[t[i] - 'a']--;
        }
        for (int i = 0; i < 26; i++) {
            if (record[i] != 0) {
                // record数组如果有的元素不为零0，说明字符串s和t 一定是谁多了字符或者谁少了字符。
                return false;
            }
        }
        // record数组所有元素都为零0，说明字符串s和t是字母异位词
        return true;
    }
};
```
Time Complexity: O(n)  
Space Complexity:O(1)  

##### Notes
If the range for the data is small, we can use the array as the Hash Table  
