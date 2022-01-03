#### #209 Minimum Size Subarray Sum
[Leetcode #209](https://leetcode.com/problems/minimum-size-subarray-sum/)  
##### My solution  
```
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int miniLen=nums.size(),flag=0;
        int sum=0;
        for(int i=0;i<nums.size();i++){
                int range=(i+miniLen<nums.size())?(i+miniLen):nums.size();
                for(int j=i;j<range;j++){
                        sum+=nums[j];
                        if(sum>=target){
                                miniLen=j-i+1;
                                flag=1;
                                break;
                        }
                }
                sum=0;
        }
            if(flag==0)return flag;
            return miniLen;
    }
};
```
Time Complexity: O(n^2)  
Space Complexity:O(1)  

##### Solution from Carl
```
class Solution {
public:
    int minSubArrayLen(int s, vector<int>& nums) {
        int result = INT32_MAX;
        int sum = 0; // 滑动窗口数值之和
        int i = 0; // 滑动窗口起始位置
        int subLength = 0; // 滑动窗口的长度
        for (int j = 0; j < nums.size(); j++) {
            sum += nums[j];
            // 注意这里使用while，每次更新 i（起始位置），并不断比较子序列是否符合条件
            while (sum >= s) {
                subLength = (j - i + 1); // 取子序列的长度
                result = result < subLength ? result : subLength;
                sum -= nums[i++]; // 这里体现出滑动窗口的精髓之处，不断变更i（子序列的起始位置）
            }
        }
        // 如果result没有被赋值的话，就返回0，说明没有符合条件的子序列
        return result == INT32_MAX ? 0 : result;
    }
};
```
Time Complexity: O(n)  
Space Complexity:O(1)  
 
##### Notes
This problem is more like a sliding window problem. Sliding window uses two pointers to locate the start and the end where the movements are very flexible and the lenghth of window is changing too.

