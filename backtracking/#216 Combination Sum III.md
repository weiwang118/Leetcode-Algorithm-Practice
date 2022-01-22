#### #216 Combination Sum III
[Leetcode #216](https://leetcode.com/problems/combination-sum-iii/)  

##### My Solution
```
class Solution {
public:
    vector<int> combinations;
    vector<vector<int>> result;
    void backtracking(int n,int k,int sum,int startIndex){
         if(combinations.size()==k){
                 if(sum==n) result.push_back(combinations);
                 return;
         }
         if(sum>=n-1) return;
         for(int i=startIndex;i<=10-k+combinations.size();i++){
                 sum+=i;
                 combinations.push_back(i);
                 backtracking(n,k,sum,i+1);
                 sum-=i;
                 combinations.pop_back();
         }
            return;
            
    }
    vector<vector<int>> combinationSum3(int k, int n) {
        backtracking(n,k,0,1);
            return result;
    }
};
```

##### Solution from Carl
```
class Solution {
private:
    vector<vector<int>> result; // 存放结果集
    vector<int> path; // 符合条件的结果
    void backtracking(int targetSum, int k, int sum, int startIndex) {
        if (sum > targetSum) { // 剪枝操作
            return; // 如果path.size() == k 但sum != targetSum 直接返回
        }
        if (path.size() == k) {
            if (sum == targetSum) result.push_back(path);
            return;
        }
        for (int i = startIndex; i <= 9 - (k - path.size()) + 1; i++) { // 剪枝
            sum += i; // 处理
            path.push_back(i); // 处理
            backtracking(targetSum, k, sum, i + 1); // 注意i+1调整startIndex
            sum -= i; // 回溯
            path.pop_back(); // 回溯
        }
    }

public:
    vector<vector<int>> combinationSum3(int k, int n) {
        result.clear(); // 可以不加
        path.clear();   // 可以不加
        backtracking(n, k, 0, 1);
        return result;
    }
};
```
