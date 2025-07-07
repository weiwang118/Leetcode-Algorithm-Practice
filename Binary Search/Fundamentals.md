# Binary Search Fundamentals
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
以上是最基础的二分搜索，但是在算法题中会有很多复杂的变形。下面会总结一些更进阶的解法。
#### Advanced Binary Search
[34.Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array)

以此经典例题为引，题目要求找到target value第一次和最后一次出现的索引。
此题的核心是找到大于等于target的第一个元素，那么在做二分查找时对于区间[left, right]应该在nums[mid]>=target的时候，不断更新right=mid-1，这样右边界就会不停地缩小，最后left停留在最左边的满足条件的位置，即第一个大于等于target的元素位置。
同理如果要找到最后一个小于等于target的元素，那么在做二分查找时对于区间[left, right]应该在nums[mid]<=target的时候，不断更新left=mid+1，这样左边界就会不停缩小，最后right停留在最右边的满足条件的位置，即最后一个小于等于target的元素。
以上两者的区别在于 nums[mid]==target的时候，缩短右边界还是左边界，如果找第一个索引，那就缩短右边，找最后一个索引，就缩短左边。

##### 写法一
```
class Solution:
    # lower_bound 返回最小的满足 nums[i] >= target 的下标 i
    # 如果数组为空，或者所有数都 < target，则返回 len(nums)
    # 要求 nums 是非递减的，即 nums[i] <= nums[i + 1]
    def lower_bound(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1  # 闭区间 [left, right]
        while left <= right:  # 区间不为空
            mid = (left + right) // 2
            if nums[mid] >= target:
                right = mid - 1  # 范围缩小到 [left, mid-1]
            else:
                left = mid + 1  # 范围缩小到 [mid+1, right]
        return left

    def searchRange(self, nums: List[int], target: int) -> List[int]:
        start = self.lower_bound(nums, target)
        if start == len(nums) or nums[start] != target:
            return [-1, -1] 
        end = self.lower_bound(nums, target + 1) - 1
        return [start, end]
```
##### 写法二
```
class Solution(object):
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        
        def binarySearch(self, nums, target, findFirst):
            left, right = 0, len(nums)-1
            idx = -1
            while (left <= right):
                mid = (left + right)//2
                if  target > nums[mid]:
                    left = mid + 1
                elif target < nums[mid]:
                    right = mid - 1
                else:
                    idx = mid
                    if findFirst: right = mid - 1
                    else: left = mid + 1
                
            return idx;

        left = binarySearch(self, nums, target, True)
        right = binarySearch(self, nums, target, False)
        return [left, right]
```

总结一下，以上算法适用于在一个不递减的数列中，找到第一个大于等于target的位置和最后一个小于等于target的位置。这种算法思想可以运用在很多场景中，比如假设有一道题算法题是 给你一个不递减的有序数列，让你插入target value到有序数列中，此时就可以照搬上面的算法，因为该算法返回的位置就是第一个大于等于target的位置。

不难发现以下例题是binary search返回的都是left，因为我们都在寻找第一个位置。
例题：[35. Search Insert Position](https://leetcode.com/problems/search-insert-position)
```
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left, right = 0, len(nums)-1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid - 1
            else:
                left = mid + 1
        return left
```

例题：[2529. Maximum Count of Positive Integer and Negative Integer](https://leetcode.com/problems/maximum-count-of-positive-integer-and-negative-integer)
```
class Solution(object):
    def maximumCount(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        def firstOccur(self, nums, target):
            left, right = 0, n - 1
            while left <= right:
                mid = (left + right)//2
                if nums[mid] >= target:
                    right = mid -1
                else: left = mid + 1
            return left
            
        firstZero = firstOccur(self, nums, 0)
        secondZero = firstOccur(self, nums, 1) - 1
        return max(firstZero, n - secondZero -1)
```
也有binary search返回right的例题：
[275. H-Index II](https://leetcode.com/problems/h-index-ii)
在此例题中，我们要寻找的是满足特定条件的最大值h-index，因此应该不断缩小左边界限，最后返回right。
```
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        # left, right 是h-index可能的范围
        left, right = 0, len(citations)
        while left <= right:
            # mid 是二分查找的值
            mid = (left + right)//2
            if mid <= citations[-mid]:
                left = mid + 1
            else:
                right = mid - 1
        
        return right
```

##### 规律
在一个非递减的有序数列中
1. Boundary
   
   left和right是二分搜索的左右边界，在大部分数列题中左闭右闭的写法是left=0,right=len(nums)-1。但也有特殊情况，比如[275. H-Index II](https://leetcode.com/problems/h-index-ii)，我们是要在0～n这个范围内寻找最大满足条件的h值，所以left和right的值应是0和n，这时left和right指向的并不是数组下标，而是h-index candidate。
   
2. Calculate the mid

   mid = (left + right)//2, 在大部分数组题中mid为下标，得出mid后再比较nums[mid]和nums[right/left]。
   
3. How to shrink the boundary
   
   最基本的二分搜索写法
   ```
   if(nums[mid]<target) left=mid+1;
   else if (nums[mid]>target) right=mid-1;
   else return mid;
   ```
   
   寻找第一个大于等于target的位置: 在nums[mid]==target时，继续缩短右边界，返回left。
   ```
   if(nums[mid]<target) left=mid+1;
   else if (nums[mid]>=target) right=mid-1;
   return left;
   ```
   
   寻找最后一个小于等于target的位置: 在nums[mid]==target时，继续缩短左边界。返回right。
   ```
   if(nums[mid]<=target) left=mid+1;
   else if (nums[mid]>target) right=mid-1;
   return right;
   ```
   
5. While loop
   ```
   while(left<=right)
   ```

这个进阶算法思想把二分搜索找到目标值扩展到了通过二分搜索找到第一个大于等于target的位置和最后一个小于等于target的位置，此种算法思想可以运用到更广泛的涉及查找的算法问题中。
