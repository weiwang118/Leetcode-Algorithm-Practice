#### #104 Maximum Depth of Binary Tree
[Leetcode #104](https://leetcode.com/problems/maximum-depth-of-binary-tree/)  

##### My Solution
Iteration
```
class Solution {
public:
    int maxDepth(TreeNode* root) {
        int ans=0;
        if(root==NULL) return ans;
        queue<TreeNode*>que;
        que.push(root);
        while(!que.empty()){
                int size=que.size();
                for(int i=0;i<size;i++){
                        TreeNode *cur=que.front();
                        que.pop();
                        if(cur->left)que.push(cur->left);
                        if(cur->right)que.push(cur->right);
                }
                ans++;
        }
            return ans;
    }
};
```
Recursion
```
class Solution {
public:
    int Traversal(TreeNode* cur){
            if(cur==NULL) return 0;
            int ldepth=Traversal(cur->left);
            int rdepth=Traversal(cur->right);
            return 1+max(ldepth,rdepth);
    }
    int maxDepth(TreeNode* root) {
      return Traversal(root);
    }
};
```
