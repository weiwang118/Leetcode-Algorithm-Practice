#### #3 Longest Substring Without Repeating Characters
##### My Solution
```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int Len=0;
        int eIndex=0;
        string newstr;
        for(int fIndex=0;fIndex<s.length();fIndex++){
        while(newstr.find(s[eIndex])==string::npos&&eIndex<s.length()){
                newstr.append(1,s[eIndex]);
                Len=Len>(eIndex-fIndex+1)?Len:(eIndex-fIndex+1);
                        eIndex++;
                }
                if(newstr.length()>1)newstr=newstr.substr(1,eIndex-fIndex);
                else newstr.clear();
        }

            return Len;
    }
    
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  

##### Solution from leetcode official
```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        // 哈希集合，记录每个字符是否出现过
        unordered_set<char> occ;
        int n = s.size();
        // 右指针，初始值为 -1，相当于我们在字符串的左边界的左侧，还没有开始移动
        int rk = -1, ans = 0;
        // 枚举左指针的位置，初始值隐性地表示为 -1
        for (int i = 0; i < n; ++i) {
            if (i != 0) {
                // 左指针向右移动一格，移除一个字符
                occ.erase(s[i - 1]);
            }
            while (rk + 1 < n && !occ.count(s[rk + 1])) {
                // 不断地移动右指针
                occ.insert(s[rk + 1]);
                ++rk;
            }
            // 第 i 到 rk 个字符是一个极长的无重复字符子串
            ans = max(ans, rk - i + 1);
        }
        return ans;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(∣Σ∣)  




