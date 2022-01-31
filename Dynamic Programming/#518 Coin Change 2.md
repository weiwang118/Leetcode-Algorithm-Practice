#### #518 Coin Change 2
[Leetcode #518](https://leetcode.com/problems/coin-change-2/)  

##### Solution from Carl
```
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        vector<int> dp(amount + 1, 0);
        dp[0] = 1;
        for (int i = 0; i < coins.size(); i++) { // 遍历物品
            for (int j = coins[i]; j <= amount; j++) { // 遍历背包
                dp[j] += dp[j - coins[i]];
            }
        }
        return dp[amount];
    }
};
```
Time Complexity: O(mn)  
Space Complexity: O(m)  

##### Notes: 
This is a complete knapsack problem!!! Also it's a combination problem!!! Traverse items first and then the knapsack. In this question, you have to fulfill the knapsack, so the formula is dp[j]+=dp[j-coins[i]].  
