#### #217 Contains Duplicate
[Leetcode #217](https://leetcode.com/problems/contains-duplicate/)  

##### My Solution
```
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> elements;
        for(int i=0;i<nums.size();i++)
                elements.insert(nums[i]);
        if(elements.size()==nums.size())
                return false;
        return true;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  

##### Leetcode Solution
```
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> elements;
        for(int i=0;i<nums.size();i++){
          if(elements.find(nums[i])!=elements.end())
                  return true;
          else elements.insert(nums[i]);       
        }
        
        return false;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  
