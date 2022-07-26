#### #238 Product of Array Except Self
[Leetcode #238](https://leetcode.com/problems/product-of-array-except-self/)  

##### My Solution
```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> result(nums.size(),1);
        vector<int> suffix(nums.size(),1);
        for(int i=1;i<nums.size();i++)
                result[i]=result[i-1]*nums[i-1];
        for(int i=nums.size()-2;i>=0;i--)
                suffix[i]=suffix[i+1]*nums[i+1];
        for(int i=0;i<nums.size();i++)
                result[i]*=suffix[i];
        return result;
                
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  

```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        
        res = [1]*len(nums)
        for i in range(0, len(nums)-1):
                res[i] = nums[i] * res[i-1] 
                
        right_product = 1
        for i in range(len(nums)-1, 0, -1): 
                res[i] = right_product * res[i-1] 
                right_product *= nums[i] 
   
        res[0] = right_product
        return res
```

##### Leetcode Solution
```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> result(nums.size(),1);
        int right_product=1;
        for(int i=1;i<nums.size();i++)
                result[i]=result[i-1]*nums[i-1];
        for(int i=nums.size()-1;i>=0;i--){
                result[i]*=right_product;
                right_product*=nums[i];
        }
        return result;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  

##### Neetcode Solution
```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = [1] * (len(nums))

        prefix = 1
        for i in range(len(nums)):
            res[i] = prefix
            prefix *= nums[i]
        postfix = 1
        for i in range(len(nums) - 1, -1, -1):
            res[i] *= postfix
            postfix *= nums[i]
        return res
```
##### Notes:
Smart Trick: Use a variable instead of a array.  
