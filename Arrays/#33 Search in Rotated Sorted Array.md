#### #33 Search in Rotated Sorted Array
[Leetcode #33](https://leetcode.com/problems/search-in-rotated-sorted-array/)  
**left side is non-rotated**  
![left side is non-rotated](https://leetcode.com/problems/search-in-rotated-sorted-array/Figures/33/33_small_mid.png)  
**right side is non-rotated**  
![right side is non-rotated](https://leetcode.com/problems/search-in-rotated-sorted-array/Figures/33/33_big_mid.png)  
##### Leetcode Solution
```
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int start=0,end=nums.size()-1;
        while(start<=end){
                int mid=start+(end-start)/2;
                if(nums[mid]==target) return mid;
                else if(nums[mid]>=nums[start]){
                        if(target>=nums[start]&&target<nums[mid])
                                end=mid-1;
                        else start=mid+1;
                }
                else{
                        if(target>nums[mid]&&target<=nums[end])
                                start=mid+1;
                        else end=mid-1;
                }
        }
            return -1;
    }
};
```
Time Complexity: O(logn)  
Space Complexity: O(1)  
