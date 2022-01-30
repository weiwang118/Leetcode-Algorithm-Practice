#### #494 Target Sum
[Leetcode #494](https://leetcode.com/problems/target-sum/)  

##### My Solution
```
class Solution {
public:
    int count=0;
    void backtracking(vector<int>& nums,int target,int startIndex,int sum){
            if(startIndex==nums.size()) {
                    if(sum==target)
                            count++;
                    return;}
            sum+=nums[startIndex];
            backtracking(nums,target,startIndex+1,sum);
            sum-=2*nums[startIndex];
            backtracking(nums,target,startIndex+1,sum);
            
    }
    int findTargetSumWays(vector<int>& nums, int target) {
        backtracking(nums,target,0,0);
            return count;
    }
};
```
Passed all test cases but time limit exceeded!!!  
Time Complexity: O(2^n)   
Space Complexity: O(n)  

##### Solution from Carl
```
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        int sum = 0;
        for (int i = 0; i < nums.size(); i++) sum += nums[i];
        if (abs(S) > sum) return 0; // 此时没有方案
        if ((S + sum) % 2 == 1) return 0; // 此时没有方案
        int bagSize = (S + sum) / 2;
        vector<int> dp(bagSize + 1, 0);
        dp[0] = 1;
        for (int i = 0; i < nums.size(); i++) {
            for (int j = bagSize; j >= nums[i]; j--) {
                dp[j] += dp[j - nums[i]];
            }
        }
        return dp[bagSize];
    }
};
```
Time Complexity: O(nm)  
Space Complexity: O(m)  
