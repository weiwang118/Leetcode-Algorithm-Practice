#### #122 Best Time to Buy and Sell Stock II
[Leetcode #122](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)  

##### My Solution
```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
            int max_profit=0;
            for(int i=1;i<prices.size();i++){
                    if(prices[i]-prices[i-1]>0)
                            max_profit+=prices[i]-prices[i-1];
            }
            return max_profit;
    }
};
```
