#### #701 Insert into a Binary Search Tree
[Leetcode #701](https://leetcode.com/problems/insert-into-a-binary-search-tree/)  

##### My Solution
```
class Solution {
public:
    TreeNode *pre=NULL;
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(root==NULL&&pre==NULL)  
        {
             root=new TreeNode(val);return root;}
        if(root==NULL)
        {       if(val<pre->val) pre->left=new TreeNode(val);
                   else pre->right=new TreeNode(val);
         return nullptr;
                }
        pre=root;
        if(root->val>val) insertIntoBST(root->left,val);
        else insertIntoBST(root->right,val);
        return root;
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if (root == NULL) {
            TreeNode* node = new TreeNode(val);
            return node;
        }
        if (root->val > val) root->left = insertIntoBST(root->left, val);
        if (root->val < val) root->right = insertIntoBST(root->right, val);
        return root;
    }
};
```
##### Notes:
The difference between two codes is whether has valid return values; Carl's code returns new node to link to their parent code.  


