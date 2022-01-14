#### #669 Trim a Binary Search Tree
[Leetcode #669](https://leetcode.com/problems/trim-a-binary-search-tree/)  

##### My Solution
```
class Solution {
public:
    TreeNode* trimBST(TreeNode* root, int low, int high) {
        if(root==nullptr) return nullptr;
        if(root->val<low) return trimBST(root->right,low,high);
        if(root->val>high)  return trimBST(root->left,low,high);
        root->left=trimBST(root->left,low,high);
        root->right=trimBST(root->right,low,high);
            return root;
    }
};
```
