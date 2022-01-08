#### #383 Ransom Note
[Leetcode #383](https://leetcode.com/problems/ransom-note/)  

##### My Solution
```
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        int hashtable[26]={0};
        for(int i=0;i<magazine.length();i++)
                hashtable[magazine[i]-'a']++;
        for(int i=0;i<ransomNote.length();i++)
        {
                if(hashtable[ransomNote[i]-'a']>0)
                        hashtable[ransomNote[i]-'a']--;
                else return false;
        }
            return true;
                 
    }
};
```
Time Complexity: O(n+m)  
Space Complexity: O(26)  

##### Solution from Carl
```
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        int record[26] = {0};
        for (int i = 0; i < magazine.length(); i++) {
            // 通过recode数据记录 magazine里各个字符出现次数
            record[magazine[i]-'a'] ++;
        }
        for (int j = 0; j < ransomNote.length(); j++) {
            // 遍历ransomNote，在record里对应的字符个数做--操作
            record[ransomNote[j]-'a']--;
            // 如果小于零说明ransomNote里出现的字符，magazine没有
            if(record[ransomNote[j]-'a'] < 0) {
                return false;
            }
        }
        return true;
    }
};
```
Time Complexity: O(n+m)  
Space Complexity: O(26)  
