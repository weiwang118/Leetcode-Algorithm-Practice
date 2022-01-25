#### #78 Subsets 
[Leetcode #78](https://leetcode.com/problems/subsets/)  

##### My Solution
```
class Solution {
public:
    vector<vector<int>> result;
    vector<int> path;
    void backtracking(vector<int>&nums,int startIndex){
                    result.push_back(path);
            for(int i=startIndex;i<nums.size();i++){
                    path.push_back(nums[i]);
                    backtracking(nums,i+1);
                    path.pop_back();
            }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
            backtracking(nums,0);
            return result;
        
    }
};
```

##### Notes:
要清楚子集问题和组合问题、分割问题的的区别，子集是收集树形结构中树的所有节点的结果。而组合问题、分割问题是收集树形结构中叶子节点的结果。  
