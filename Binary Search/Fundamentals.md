# Binary Search Fundamentals

### 2021.12.28 Update

Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing in half the portion of the list that could contain the item, until you've narrowed down the possible locations to just one.

Some of the most common problems include:  
Infinity loop  
Can't decide where to shrink  
Do I use left or right  
When to exit the loop  
...  
#### The Pattern
我们定义 target 是在一个在左闭右闭的区间里，也就是[left, right] （这个很重要非常重要）。  
区间的定义这就决定了二分法的代码应该如何写，因为定义target在[left, right]区间，所以有如下两点：  
while (left <= right) 要使用 <= ，因为left == right是有意义的，所以使用 <=  
if (nums[middle] > target) right 要赋值为 middle - 1，因为当前这个nums[middle]一定不是target，那么接下来要查找的左区间结束下标位置就是 middle - 1  

1. Boundary
   choice of left and right: we normally set it to the original range of the array  
   ```
   left=0;right=nums.size()-1;
   ```
   This is not always the case, sometimes may change on the special case.

2. Calculate the mid
   ```
   mid = (left+right)/2 // worst, very easy to overflow

   mid = left+(right-left)/2 // much better, but still possible

   mid = (left + right) >>> 1 // the best, but hard to understand
   ```
3. How to shrink the boundary
   ```
   if(nums[mid]<target) left=mid+1;
   else if (nums[mid]>target) right=mid-1;
   else return mid;
   ```
4. While loop
   ```
   while(left<=right)
   ```
  #### Leetcode 704
 Problem Link: https://leetcode.com/problems/binary-search/
  ```
  class Solution {
  public:
  int search(vector<int>& nums, int target) {
    int pivot, left = 0, right = nums.size() - 1;
    while (left <= right) {
      pivot = left + (right - left) / 2;
      if (nums[pivot] == target) return pivot;
      if (target < nums[pivot]) right = pivot - 1;
      else left = pivot + 1;
    }
    return -1;
  }
};
  ```
  ##### Java Solution
  ```
  class Solution {
    public int search(int[] nums, int target) {
        int left=0,right=nums.length-1;
        while(left<=right){
                int mid=left+(right-left)/2;
                if(nums[mid]==target)
                        return mid;
                else if(target<nums[mid]){
                        right=mid-1;
                }
                else left=mid+1;
        }
            return -1;
    }
}
  ```
  Time Complexity: O(logn)  
  Space Complexity: O(1)  
