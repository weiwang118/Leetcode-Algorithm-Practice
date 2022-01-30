#### #1049 Last Stone Weight II
[Leetcode #1049](https://leetcode.com/problems/last-stone-weight-ii/)  

##### My Solution 
```
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        int sum=0;
        for(int i=0;i<stones.size();i++)
                sum+=stones[i];
        int target=sum/2;
        vector<int> dp(target+1,0);
        for(int i=0;i<stones.size();i++){
                for(int j=target;j>=stones[i];j--){
                        dp[j]=max(dp[j],dp[j-stones[i]]+stones[i]);
                }
        }
            return sum-dp[target]-dp[target];
    }
};
```
Time Complexity: O(mn)  
Space Complexity: O(m)  
