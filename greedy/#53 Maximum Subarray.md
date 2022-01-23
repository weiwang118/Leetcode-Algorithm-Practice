#### #53 Maximum Subarray
[Leetcode #53](https://leetcode.com/problems/maximum-subarray/)  

##### My Solution
```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int sum=0;
        int maxSum=INT32_MIN;
        for(int i=0;i<nums.size();i++){
                sum+=nums[i];
                maxSum=sum>maxSum?sum:maxSum;
                if(sum<0)sum=0;
        }
            return maxSum;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  

