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
