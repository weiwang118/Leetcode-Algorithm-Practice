#### #404 Sum of Left Leaves
[Leetcode #404](https://leetcode.com/problems/sum-of-left-leaves/)  

##### My Solution
```
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
        if(root==NULL) return 0;
        queue<TreeNode*> que;
        que.push(root);
        int sum=0;
        while(!que.empty()){
                TreeNode *cur=que.front();que.pop();
                if(cur->left) {
                        que.push(cur->left);
                         if(!cur->left->left && !cur->left->right)
                               sum+=cur->left->val;}
                if(cur->right) que.push(cur->right);
               
        }
            return sum;
    }
};
```

##### Solution from Carl
Recursion
```
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
        if (root == NULL) return 0;
        int midValue = 0;
        if (root->left != NULL && root->left->left == NULL && root->left->right == NULL) {
            midValue = root->left->val;
        }
        return midValue + sumOfLeftLeaves(root->left) + sumOfLeftLeaves(root->right);
    }
};
```
