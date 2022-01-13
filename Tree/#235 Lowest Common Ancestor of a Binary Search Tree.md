#### #235 Lowest Common Ancestor of a Binary Search Tree
[Leetcode #235](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)  

##### My Solution
If this is just a binary tree, we can tranverse it in postorder.  
```
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root==p||root==q||root==NULL) return root;
        TreeNode* left=lowestCommonAncestor(root->left,p,q);
        TreeNode* right=lowestCommonAncestor(root->right,p,q);
            if(left!=NULL&&right==NULL)
                    return left;
            else if(left==NULL&&right!=NULL)
                    return right;
            else if(left!=NULL&&right!=NULL)
                    return root;
            else return NULL;
    }
};
```

But it is a binary search tree, we should use the nature of it.  
Recursion  
```
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(p->val<root->val&&q->val<root->val) 
                return lowestCommonAncestor(root->left,p,q);
         else if (p->val>root->val&&q->val>root->val) 
                 return lowestCommonAncestor(root->right,p,q);
            return root;
    }
};
```

Iteration  
```
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
     while(root){
             if(p->val>root->val&&q->val>root->val)
                     root=root->right;
             else if(p->val<root->val&&q->val<root->val)
                     root=root->left;
             else return root;
     }
            return NULL;
    }
};
```
