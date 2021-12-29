#### #35 Search Insert Position
[Leetcode#35](https://leetcode.com/problems/search-insert-position/)
```
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left=0,n=nums.size()-1,pivot,right;
        right=n;
        while(left<=right){
                pivot=left+(right-left)/2;
                if(nums[pivot]<target)left=pivot+1;
                else if(nums[pivot]>target)right=pivot-1;
                else return pivot;
        }
        // 分别处理如下四种情况
        // 目标值在数组所有元素之前  [0, -1]
        // 目标值等于数组中某一个元素  return middle;
        // 目标值插入数组中的位置 [left, right]，return  right + 1
        // 目标值在数组所有元素之后的情况 [left, right]， return right + 1
        return right+1;
    }
};
```
Time Complexity: O(logn)  
Space Complexity: O(1)
