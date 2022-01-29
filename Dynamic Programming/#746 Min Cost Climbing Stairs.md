#### #746 Min Cost Climbing Stairs
[Leetcode #746](https://leetcode.com/problems/min-cost-climbing-stairs/)  

##### My Solution
```
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int cost1=0,cost2=0;
        int ans;
        for(int i=2;i<=cost.size();i++){
                ans=min(cost1+cost[i-1],cost2+cost[i-2]);
                cost2=cost1;
                cost1=ans;
        }
            return ans;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
