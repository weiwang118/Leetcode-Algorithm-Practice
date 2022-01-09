#### #107 Binary Tree Level Order Traversal II
[Leetcode #107](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)  

##### My Solution
```
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> ans;
        queue<TreeNode*> que;
        if(root!=NULL) que.push(root);
         while(!que.empty()){
                 int size=que.size();
                 vector<int>vec;
                 for(int i=0;i<size;i++){
                         TreeNode*cur=que.front();
                         que.pop();
                         vec.push_back(cur->val);
                         if(cur->left)que.push(cur->left);
                         if(cur->right)que.push(cur->right);
                 }
                 ans.push_back(vec);
         }
            reverse(ans.begin(),ans.end());
            return ans;
    }
};
```
