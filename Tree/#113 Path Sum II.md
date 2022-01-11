#### #113 Path Sum II
[Leetcode #113](https://leetcode.com/problems/path-sum-ii/)  

##### My Solution
```
class Solution {
public:
    vector<vector<int>> ans;
    void getSum(TreeNode*root, int sum,vector<int> vec){
            if(root==NULL) return;
            vec.push_back(root->val);
            if(!root->left&&!root->right&&root->val==sum)
                  ans.push_back(vec);
            getSum(root->left,sum-root->val,vec);
            getSum(root->right,sum-root->val,vec);
    }
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
         vector<int> vec;
         getSum(root,targetSum,vec);
         return ans;
    }
};
```
