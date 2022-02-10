#### #121 Best Time to Buy and Sell Stock
[Leetcode #121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)  

##### My Solution
```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int max_profit=0;
        int p0=0;
        for(int i=1;i<prices.size();i++){
                p0=max((prices[i]-prices[i-1]+p0),0);
                max_profit=max(max_profit,p0);
        }
            return max_profit;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  

##### Notes:
在这样的一段连续价格区间内，因为购买和售出只能有一次，所以要选择唯一的最低点和唯一的最高点，用P0来累计利润，而当P0小于0时应该抛弃前面所有的计算（因为此时出现了新的最低点），重置为0. 但凡P0仍为正数（说明没有出现更低点），那么旧P0就应该用来算新P0.这样就算出了所有可能的利润，将最大值存储在max_Profit中。  

##### Leetcode Solution
```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int max_profit=0;
        int min_price=prices[0];
        for(int i=1;i<prices.size();i++){
                if(prices[i]<min_price)
                        min_price=prices[i];
                else{
                        max_profit=max(max_profit,prices[i]-min_price);
                }
        }
            return max_profit;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
