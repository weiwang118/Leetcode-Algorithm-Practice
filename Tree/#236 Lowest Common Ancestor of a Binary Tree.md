#### #236 Lowest Common Ancestor of a Binary Tree
[Leetcode #236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)  

##### My Solution
```
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root==q||root==p||root==NULL) return root;
        TreeNode *left=lowestCommonAncestor(root->left,p,q);
        TreeNode *right=lowestCommonAncestor(root->right,p,q);
         
        if(left!=NULL&&right!=NULL) return root;
         else if(left!=NULL&&right==NULL) return left;
            else if(left==NULL&&right!=NULL) return right;
            else return NULL;
    }
};
```
Notes: Use postorder traverse the binary tree from bottom to top and find the lowest common ancestor of it.  
