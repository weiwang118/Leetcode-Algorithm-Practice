#### #34 Find First and Last Position of Element in Sorted Array
[Leetcode #34](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)  

##### My Solution
```
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int left=0;
        int right=nums.size()-1;
        int pivot,loc1=-1,loc2=-1;
        while(left<=right){
                pivot=left+(right-left)/2;
                if(nums[pivot]<target)left=pivot+1;
                else if(nums[pivot]>target)right=pivot-1;
                else{
                        for(int i=left;i<=right;i++){
                                if(nums[i]==target) {
                                        loc1=i;      
                                        break;      }}   
                        for(int i=right;i>=left;i--){
                                if(nums[i]==target) {
                                        loc2=i;      
                                        break;      }}
                        
                        return {loc1,loc2};
                }
        }
            return {loc1,loc2};
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int leftBorder = getLeftBorder(nums, target);
        int rightBorder = getRightBorder(nums, target);
        // 情况一
        if (leftBorder == -2 || rightBorder == -2) return {-1, -1};
        // 情况三
        if (rightBorder - leftBorder > 1) return {leftBorder + 1, rightBorder - 1};
        // 情况二
        return {-1, -1};
    }
private:
     int getRightBorder(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        int rightBorder = -2; // 记录一下rightBorder没有被赋值的情况
        while (left <= right) {
            int middle = left + ((right - left) / 2);
            if (nums[middle] > target) {
                right = middle - 1;
            } else { // 寻找右边界，nums[middle] == target的时候更新left
                left = middle + 1;
                rightBorder = left;
            }
        }
        return rightBorder;
    }
    int getLeftBorder(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        int leftBorder = -2; // 记录一下leftBorder没有被赋值的情况
        while (left <= right) {
            int middle = left + ((right - left) / 2);
            if (nums[middle] >= target) { // 寻找左边界，nums[middle] == target的时候更新right
                right = middle - 1;
                leftBorder = right;
            } else {
                left = middle + 1;
            }
        }
        return leftBorder;
    }
};
```
Time Complexity: O(logn)  
Space Complexity: O(1)  
