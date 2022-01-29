#### #62 Unique Paths
[Leetcode #62](https://leetcode.com/problems/unique-paths/)  

##### My Solution
```
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int>(n,1));
        for(int i=1;i<m;i++){
                for(int j=1;j<n;j++){
                        dp[i][j]=dp[i-1][j]+dp[i][j-1];
                }
        }
            return dp[m-1][n-1];
    }
};
```
Time Complexity: O(m×n)  
Space Complexity: O(m×n)  

##### Solution from Carl
```
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> dp(n);
        for (int i = 0; i < n; i++) dp[i] = 1;
        for (int j = 1; j < m; j++) {
            for (int i = 1; i < n; i++) {
                dp[i] += dp[i - 1];
            }
        }
        return dp[n - 1];
    }
};
```
Time Complexity: O(m×n)  
Space Complexity: O(n)  
