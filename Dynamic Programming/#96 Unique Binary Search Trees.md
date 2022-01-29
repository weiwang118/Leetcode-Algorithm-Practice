#### #96 Unique Binary Search Trees
[Leetcode #96](https://leetcode.com/problems/unique-binary-search-trees/)  

##### Solution from Carl
```
class Solution {
public:
    int numTrees(int n) {
        vector<int> dp(n + 1);
        dp[0] = 1;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                dp[i] += dp[j - 1] * dp[i - j];
            }
        }
        return dp[n];
    }
};
```
Time Complexity: O(n^2)  
Space Complexity: O(n)  

##### Notes:
Although this is a medium question on Leetcode, I think it's actually hard level.  
[More explanation from Carl](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0096.%E4%B8%8D%E5%90%8C%E7%9A%84%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.md)  

