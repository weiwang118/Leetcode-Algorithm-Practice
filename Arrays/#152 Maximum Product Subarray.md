#### #152 Maximum Product Subarray
[Leetcode #152](https://leetcode.com/problems/maximum-product-subarray/)  

##### Leetcode Solution
```
class Solution {
public:
    int maxProduct(vector<int>& nums) {
       if(nums.size()==0) return 0;
       int max_cur=nums[0];
       int min_cur=nums[0];
        int result=max_cur;
        for(int i=1;i<nums.size();i++){
                int curr=nums[i];
                int temp_max=max(curr,max(max_cur*curr,min_cur*curr));
                min_cur=min(curr,min(max_cur*curr,min_cur*curr));
                max_cur=temp_max;
                result=max(max_cur,result);
        }
            return result;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
##### Notes:
The most difficult part is how to handle the negative numbers. Use min_cur to store all the possible negative results and keep comparing with other results.  
