#### #1 Two Sum
[Leetcode #1](https://leetcode.com/problems/two-sum/)

##### My Solution
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
            unordered_map<int,int> _map;
            int i;
            for( i=0;i<nums.size();i++)
                    _map.insert({nums[i],i});
            unordered_map<int,int>:: iterator it;
            // can change to "auto it=map.find(target-nums[i])"
            for( i=0;i<nums.size();i++){
                    it=_map.find(target-nums[i]);
                    if(it!=_map.end()&&it->second!=i)
                           break;
                            
            }
            return {i,it->second};
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  

![](https://code-thinking.cdn.bcebos.com/gifs/1.两数之和.gif)  
##### Solution from Carl
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::unordered_map <int,int> map;
        for(int i = 0; i < nums.size(); i++) {
            auto iter = map.find(target - nums[i]);
            if(iter != map.end()) {
                return {iter->second, i};
            }
            map.insert(pair<int, int>(nums[i], i));
        }
        return {};
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  
