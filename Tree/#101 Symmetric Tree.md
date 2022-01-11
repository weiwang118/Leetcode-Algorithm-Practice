#### #101 Symmetric Tree
[Leetcode #101](https://leetcode.com/problems/symmetric-tree/)  

##### My Solution
Recursion
```
class Solution {
public:
    bool Compare(TreeNode *left,TreeNode *right){
            if(left!=NULL && right==NULL) return false;
            else if(left==NULL&& right!=NULL) return false;
            else if(left==NULL && right==NULL) return true;
            else if(left->val!=right->val) return false;
            
            bool Outside=Compare(left->left,right->right);
            bool Inside=Compare(left->right,right->left);
            if(Outside&&Inside) return true;
            return false;
            
    }
        
    bool isSymmetric(TreeNode* root) {
        if(root==NULL) return true;
        return Compare(root->left,root->right);
    }
};
```

Iteration
```
class Solution {
public: 
    bool isSymmetric(TreeNode* root) {
        queue<TreeNode*> que;
        if(root==NULL) return true;
        que.push(root->left);
        que.push(root->right);
        while(!que.empty()){
                TreeNode* left=que.front();que.pop();
                TreeNode* right=que.front();que.pop();
                if(!left&&!right)
                        continue;
                
                if(!left || !right || left->val!=right->val)
                        return false;
                que.push(left->left);
                que.push(right->right);
                que.push(left->right);
                que.push(right->left);
        }
            return true;
    }
};
```

