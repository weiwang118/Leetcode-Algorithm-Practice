#### #111 Minimum Depth of Binary Tree
[Leetcode #111](https://leetcode.com/problems/minimum-depth-of-binary-tree/)  

##### My Solution
```
class Solution {
public:
    int minDepth(TreeNode* root) {
        int ans=0;
        if(root==NULL) return ans;
        queue<TreeNode*>que;
        que.push(root);
        while(!que.empty()){
                int size=que.size();
                ans++;
                for(int i=0;i<size;i++){
                        TreeNode *cur=que.front();
                        que.pop();
                        if(!cur->left&&!cur->right) return ans;
                        if(cur->left)que.push(cur->left);
                        if(cur->right)que.push(cur->right);
                }
        }
            return ans;
    }
};
```
