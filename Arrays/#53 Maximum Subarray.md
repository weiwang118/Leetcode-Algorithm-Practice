#### #53 Maximum Subarray
[Leetcode #53](https://leetcode.com/problems/maximum-subarray/)  

##### My Solution
```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max_sum=INT32_MIN;
        int cur_sum=0;
        for(int i=0;i<nums.size();i++){
                cur_sum+=nums[i];
                if(cur_sum>max_sum)
                        max_sum=cur_sum;
                if(cur_sum<0) cur_sum=0;
        }
            return max_sum;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  

##### Notes:
It's kind of greedy. When the sum is negative, throw it away!! Calculate the new sum from next element. When traverse the array, store the max sum in the max_sum variable.  

##### Leetcode Solution: Divide and Conquer  
[Solutions](https://leetcode-cn.com/problems/maximum-subarray/solution/zui-da-zi-xu-he-by-leetcode-solution/)  
```
class Solution {
public:
    struct Status {
        int lSum, rSum, mSum, iSum;
    };

    Status pushUp(Status l, Status r) {
        int iSum = l.iSum + r.iSum;
        int lSum = max(l.lSum, l.iSum + r.lSum);
        int rSum = max(r.rSum, r.iSum + l.rSum);
        int mSum = max(max(l.mSum, r.mSum), l.rSum + r.lSum);
        return (Status) {lSum, rSum, mSum, iSum};
    };

    Status get(vector<int> &a, int l, int r) {
        if (l == r) {
            return (Status) {a[l], a[l], a[l], a[l]};
        }
        int m = (l + r) >> 1;
        Status lSub = get(a, l, m);
        Status rSub = get(a, m + 1, r);
        return pushUp(lSub, rSub);
    }

    int maxSubArray(vector<int>& nums) {
        return get(nums, 0, nums.size() - 1).mSum;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(logn)  
