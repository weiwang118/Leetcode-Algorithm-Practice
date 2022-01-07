#### ##349 Intersection of Two Arrays
[Leetcode #349](https://leetcode.com/problems/intersection-of-two-arrays/)  

##### My Solution
```
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> nums(nums1.begin(),nums1.end());
        unordered_set<int> result;
        for(int num:nums2){
                if(nums.find(num)!=nums.end()){
                        result.insert(num);
                }
        }
            return vector<int>(result.begin(),result.end());
        
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result_set; // 存放结果
        unordered_set<int> nums_set(nums1.begin(), nums1.end());
        for (int num : nums2) {
            // 发现nums2的元素 在nums_set里又出现过
            if (nums_set.find(num) != nums_set.end()) {
                result_set.insert(num);
            }
        }
        return vector<int>(result_set.begin(), result_set.end());
    }
};
```

##### Notes:
In this situation, we can not use array as the Hash Table because there is no range for numbers in nums1 and nums2. If we use array, then waste a lot of space  
