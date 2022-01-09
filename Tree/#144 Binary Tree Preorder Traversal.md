#### #144 Binary Tree Preorder Traversal
[Leetcode #144](https://leetcode.com/problems/binary-tree-preorder-traversal/)  
##### My Solution
```
//Iteration
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        stack<TreeNode*> st;
        if(root==NULL)return ans;
        st.push(root);
        while(!st.empty()){
                TreeNode* cur=st.top();
                st.pop();
                ans.push_back(cur->val);
                if(cur->right)st.push(cur->right);
                if(cur->left)st.push(cur->left);
                
        }
            return ans;
        
    }
};
```

```
Recursion
class Solution {
public:
    void Traversal(TreeNode *cur, vector<int> &vec){
                if(cur==NULL)return;
                vec.push_back(cur->val);
                Traversal(cur->left,vec);
                Traversal(cur->right,vec);
        }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        Traversal(root,ans);
        return ans;
    }
};
```
