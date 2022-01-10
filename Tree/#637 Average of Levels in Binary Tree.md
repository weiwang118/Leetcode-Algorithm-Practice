#### #637 Average of Levels in Binary Tree
[Leetcode #637](https://leetcode.com/problems/average-of-levels-in-binary-tree/)  

##### My Solution
```
class Solution {
public:
    vector<double> averageOfLevels(TreeNode* root) {
        vector<double> ans;
        queue<TreeNode*> que;
        if(root==NULL) return ans;
        que.push(root);
        while(!que.empty()){
                int size=que.size();
                double sum=0;
                for(int i=0;i<size;i++){
                        TreeNode*cur=que.front();
                        que.pop();
                        sum+=cur->val;
                        if(cur->left)que.push(cur->left);
                        if(cur->right)que.push(cur->right);
                }
                ans.push_back(sum/size);
         }
            return ans;
    }
};
```
