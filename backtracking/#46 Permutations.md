#### #46 Permutations
[Leetcode #46](https://leetcode.com/problems/permutations/)  

##### My Solution
```
class Solution {
public:
    vector<vector<int>> result;
    vector<int> path;
    void backtracking(vector<int> nums,int len){
            if(path.size()==len){
                    result.push_back(path);
                    return ;
            }
            for(int i=0;i<nums.size();i++){
                    path.push_back(nums[i]);
                    vector<int> temp(nums.begin(),nums.end());
                    temp.erase(temp.begin()+i);
                    backtracking(temp,len);
                    path.pop_back();
            }
    }
    vector<vector<int>> permute(vector<int>& nums) {
            int len=nums.size();
            backtracking(nums,len);
            return result;
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    vector<vector<int>> result;
    vector<int> path;
    void backtracking (vector<int>& nums, vector<bool>& used) {
        // 此时说明找到了一组
        if (path.size() == nums.size()) {
            result.push_back(path);
            return;
        }
        for (int i = 0; i < nums.size(); i++) {
            if (used[i] == true) continue; // path里已经收录的元素，直接跳过
            used[i] = true;
            path.push_back(nums[i]);
            backtracking(nums, used);
            path.pop_back();
            used[i] = false;
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        result.clear();
        path.clear();
        vector<bool> used(nums.size(), false);
        backtracking(nums, used);
        return result;
    }
};
```
