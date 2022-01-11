#### #112 Path Sum
[Leetcode #112](https://leetcode.com/problems/path-sum/)  

##### My Solution
Recursion
```
class Solution {
public:
    bool getSum(TreeNode *root, int target,int sum){
            if(root==NULL) return false;
            sum+=root->val;
            if(!root->left&&!root->right){
                    if(sum==target) return true;
                    return false;
            }
return getSum(root->left,target,sum)||getSum(root->right,target,sum);
            
    }
        
    bool hasPathSum(TreeNode* root, int targetSum) {
        return getSum(root,targetSum,0);
    }
};
```

#### Solution from Carl
```
class solution {
public:
    bool haspathsum(treenode* root, int sum) {
        if (root == null) return false;
        if (!root->left && !root->right && sum == root->val) {
            return true;
        }
        return haspathsum(root->left, sum - root->val) || haspathsum(root->right, sum - root->val);
    }
};
```
