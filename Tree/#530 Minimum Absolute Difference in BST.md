#### #530 Minimum Absolute Difference in BST
[Leetcode #530](https://leetcode.com/problems/minimum-absolute-difference-in-bst/)  

##### My Solution
The binary search tree is in increasing order when traverse inorderly.

Recursion  
```
class Solution {
private:
    int min=INT_MAX;
    TreeNode *pre;
public:
    int getMinimumDifference(TreeNode* root) {
        if(root==NULL) return min;
        getMinimumDifference(root->left);
        if(pre!=NULL) min=(root->val-pre->val)<min?abs(pre->val-root->val):min;
        pre=root;
        getMinimumDifference(root->right);
        return min;
        
    }
};
```

Iteration
```
class Solution {
public:
    int getMinimumDifference(TreeNode* root) {
       stack<TreeNode*> st;
       TreeNode *cur=root;
       TreeNode *pre=NULL;
       int _min=INT_MAX;
       while(cur||!st.empty()){
               if(cur){
                       st.push(cur);
                       cur=cur->left;
               }
               else{
                     cur=st.top();
                     st.pop();
                     if(pre!=NULL)
                             _min=min(cur->val-pre->val,_min);
                     pre=cur;
                     cur=cur->right;
               }
       }
            return _min;
    }
};
```
