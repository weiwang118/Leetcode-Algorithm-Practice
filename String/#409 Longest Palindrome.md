#### #409 Longest Palindrome
[Leetcode #409](https://leetcode.com/problems/longest-palindrome/)  

##### Solution from Carl
```
class Solution {
public:
    int longestPalindrome(string s) {
        unordered_map <int,int> map;
        for(int i=0;i<s.size();i++){
                map[s[i]]++;
        }
        int ans=0;
        for(auto i=map.begin();i!=map.end();i++)
                       ans+=(i->second/2)*2;
            if(ans<s.size())
                    ans++;
            return ans;
    }
};
```

##### Solution from CYC
```
public int longestPalindrome(String s) {
    int[] cnts = new int[256];
    for (char c : s.toCharArray()) {
        cnts[c]++;
    }
    int palindrome = 0;
    for (int cnt : cnts) {
        palindrome += (cnt / 2) * 2;
    }
    if (palindrome < s.length()) {
        palindrome++;   // 这个条件下 s 中一定有单个未使用的字符存在，可以把这个字符放到回文的最中间
    }
    return palindrome;
}
```
