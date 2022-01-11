#### #513 Find Bottom Left Tree Value
[Leetcode #513](https://leetcode.com/problems/find-bottom-left-tree-value/)  

##### My Solution
Iteration
```
class Solution {
public:
    int findBottomLeftValue(TreeNode* root) {
        queue<TreeNode*> que;
        if(root!=NULL)que.push(root);
        int leftvalue=0;
        while(!que.empty()){
                int size=que.size();
                for(int i=0;i<size;i++){
                        TreeNode*cur=que.front();que.pop();
                        if(cur->left) que.push(cur->left);
                        if(cur->right)que.push(cur->right);
                        if(i==0)leftvalue=cur->val;
                }
        }
            return leftvalue;
        
    }
};
```

##### Solution from Carl
Recursion
```
class Solution {
public:
    int maxLen = INT_MIN;
    int maxleftValue;
    void traversal(TreeNode* root, int leftLen) {
        if (root->left == NULL && root->right == NULL) {
            if (leftLen > maxLen) {
                maxLen = leftLen;
                maxleftValue = root->val;
            }
            return;
        }
        if (root->left) {
            traversal(root->left, leftLen + 1); // 隐藏着回溯
        }
        if (root->right) {
            traversal(root->right, leftLen + 1); // 隐藏着回溯
        }
        return;
    }
    int findBottomLeftValue(TreeNode* root) {
        traversal(root, 0);
        return maxleftValue;
    }
};
```
