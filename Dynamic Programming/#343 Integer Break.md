#### #343 Integer Break
[Leetcode #343](https://leetcode.com/problems/integer-break/)  

##### Solution from Carl
```
class Solution {
public:
    int integerBreak(int n) {
        vector<int> dp(n + 1);
        dp[2] = 1;
        for (int i = 3; i <= n ; i++) {
            for (int j = 1; j < i - 1; j++) {
                dp[i] = max(dp[i], max((i - j) * j, dp[i - j] * j));
            }
        }
        return dp[n];
    }
};
```
Time Complexity: O(n^2)  
Space Complexity: O(n)  
