#### #199 Binary Tree Right Side View
[Leetcode #199](https://leetcode.com/problems/binary-tree-right-side-view/)  

##### My Solution
```
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
            vector<int> ans;
            queue<TreeNode*> que;
            if(root!=NULL) que.push(root);
            while(!que.empty()){
                    int size=que.size();
                    for(int i=0;i<size;i++){
                            TreeNode *cur=que.front();
                            que.pop();
                            if(i==size-1) ans.push_back(cur->val);
                            if(cur->left)que.push(cur->left);
                            if(cur->right)que.push(cur->right);
                    }
            }
            return ans;
      
    }
};
```
