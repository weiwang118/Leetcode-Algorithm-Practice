#### #416 Partition Equal Subset Sum
[Leetcode #416](https://leetcode.com/problems/partition-equal-subset-sum/)  

##### My Solution
```
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum=0;
        for(int i=0;i<nums.size();i++){
                sum+=nums[i];
        }
        if(sum%2!=0) return false;
        else sum=sum/2;
        vector<vector<int>> dp(nums.size(),vector<int>(sum+1,0));
        for(int i=1;i<=sum;i++){
                if(nums[0]<=i) dp[0][i]=nums[0];
        }
        for(int i=1;i<nums.size();i++){
                for(int j=1;j<=sum;j++){
                        if(j<nums[i])  dp[i][j]=dp[i-1][j];
                                else dp[i][j]=max(dp[i-1][j],dp[i-1][j-nums[i]]+nums[i]);
                }
        }
                if(dp[nums.size()-1][sum]==sum) return true;
                                return false;
    }
};
```
Time Complexity: O(n^2)  
Space Complexity: O(n^2)  

```
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum=0;
        for(int i=0;i<nums.size();i++){
                sum+=nums[i];
        }
        if(sum%2!=0) return false;
        else sum=sum/2;
        vector<int> dp(sum+1,0);
        for(int i=1;i<=sum;i++){
                if(nums[0]<=i) dp[i]=nums[0];
        }
        for(int i=1;i<nums.size();i++){
                for(int j=sum;j>=1;j--){
                        if(j>=nums[i]) 
                             dp[j]=max(dp[j],dp[j-nums[i]]+nums[i]);
                }
        }
                if(dp[sum]==sum) return true;
                                return false;
    }
};
```
Time Complexity: O(n^2)  
Space Complexity: O(n)  
