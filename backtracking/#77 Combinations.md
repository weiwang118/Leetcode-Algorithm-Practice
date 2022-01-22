#### #77 Combinations
[Leetcode #77](https://leetcode.com/problems/combinations/)  

##### Solution from Carl  
```
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    void backtracking(int n,int k, int startIndex){
        if(path.size()==k){
                ans.push_back(path);
                return;
        }
        for(int i=startIndex;i<=n;i++){
                path.push_back(i);
                backtracking(n,k,i+1);
                path.pop_back();
        }
    }
    vector<vector<int>> combine(int n, int k) {
        backtracking(n,k,1);
            return ans;
    }
};
```
Time Complexity: O(kC(n,k))  
Space Complexity: O(C(n,k))  
