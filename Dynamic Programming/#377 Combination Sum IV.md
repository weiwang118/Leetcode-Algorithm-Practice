#### #377 Combination Sum IV
[Leetcode #377](https://leetcode.com/problems/combination-sum-iv/)  

##### Solution from Carl
```
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<unsigned long long> dp(target + 1, 0);
        dp[0] = 1;
        for (int i = 0; i <= target; i++) { // 遍历背包
            for (int j = 0; j < nums.size(); j++) { // 遍历物品
                if (i - nums[j] >= 0) {
                    dp[i] += dp[i - nums[j]];
                }
            }
        }
        return dp[target];
    }
};

```

##### Notes:
This is a permutation problem!!!! Traverse the knapsack first and then the items!!!   
