#### #491 Increasing Subsequences
[Leetcode #491](https://leetcode.com/problems/increasing-subsequences/)  

##### My Solution
```
class Solution {
public:
    vector<vector<int>> result;
    vector<int> path;
    void backtracking(vector<int>&nums, int startIndex){
        if(path.size()>1)
                result.push_back(path);
        unordered_set<int> uset;
            for(int i=startIndex;i<nums.size();i++){
                    if(uset.find(nums[i])!=uset.end())
                            continue;
                    if(!path.empty()&&nums[i]<path.back())
                            continue;
                    uset.insert(nums[i]);
                    path.push_back(nums[i]);
                    backtracking(nums,i+1);
                    path.pop_back();
            }
    }
        
    vector<vector<int>> findSubsequences(vector<int>& nums) {
        backtracking(nums,0);
            return result;
    }
};
```

##### Solution from Carl
As we disscussed before, many data structures can be used as Hash table including set,map and array. If there is no huge data, we can use array to save space.  
```
// 版本二
class Solution {
private:
    vector<vector<int>> result;
    vector<int> path;
    void backtracking(vector<int>& nums, int startIndex) {
        if (path.size() > 1) {
            result.push_back(path);
        }
        int used[201] = {0}; // 这里使用数组来进行去重操作，题目说数值范围[-100, 100]
        for (int i = startIndex; i < nums.size(); i++) {
            if ((!path.empty() && nums[i] < path.back())
                    || used[nums[i] + 100] == 1) {
                    continue;
            }
            used[nums[i] + 100] = 1; // 记录这个元素在本层用过了，本层后面不能再用了
            path.push_back(nums[i]);
            backtracking(nums, i + 1);
            path.pop_back();
        }
    }
public:
    vector<vector<int>> findSubsequences(vector<int>& nums) {
        result.clear();
        path.clear();
        backtracking(nums, 0);
        return result;
    }
};
```
