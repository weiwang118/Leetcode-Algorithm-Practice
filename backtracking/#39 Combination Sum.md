#### #39 Combination Sum
[Leetcode #39](https://leetcode.com/problems/combination-sum/)  

##### My Solution
```
class Solution {
public:
    vector<int> path;
    vector<vector<int>> result;
    void backtracking(vector<int>& candidates, int target,int sum, int startIndex){
            if(sum==target) {
                    result.push_back(path);
                    return;
            }
            else if(sum>target) return;
            for(int i=startIndex;i<candidates.size();i++){
                    path.push_back(candidates[i]);
                    sum+=candidates[i];
                    backtracking(candidates,target,sum,i);
                    path.pop_back();
                    sum-=candidates[i];
            }
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
          backtracking(candidates,target,0,0);
            return result;
    }
};
```
