#### #153 Find Minimum in Rotated Sorted Array
[Leetcode #153](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)  

##### My Solution
```
class Solution {
public:
    int findMin(vector<int>& nums) {
        int min=nums[0];
        int left=0,right=nums.size()-1;
        while(left<=right){
                int mid=left+(right-left)/2;
                if(nums[mid]>=min)
                        left=mid+1;
                else {
                        min=nums[mid];
                        right=mid-1;
                }
        }
            return min;
    }
};
```
Time Complexity: O(logn)  
Space Complexity: O(1)  

##### Leetcode Solution
```
class Solution {
public:
    int findMin(vector<int>& nums) {
        if(nums.size()==1)
                return nums[0];
        int left=0,right=nums.size()-1;
        if(nums[right]>nums[0])
                return nums[0];
        while(left<=right){
                int mid=left+(right-left)/2;
                if(nums[mid]>nums[mid+1])
                        return nums[mid+1];
                if(nums[mid-1]>nums[mid])
                        return nums[mid];
                if(nums[mid]>nums[0])
                        left=mid+1;
                else right=mid-1;
        }
            return -1;
    }
};
```
