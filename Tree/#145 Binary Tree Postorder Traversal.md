#### #145 Binary Tree Postorder Traversal
[Leetcode #145](https://leetcode.com/problems/binary-tree-postorder-traversal/)  

##### My Solution
```
Recursion
class Solution {
public:
        void Traversal(TreeNode *cur, vector<int> &vec){
                if(cur==NULL)return;
                Traversal(cur->left,vec);
                Traversal(cur->right,vec);
                vec.push_back(cur->val);
        }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
         Traversal(root,ans);
            return ans;
    }
};
```

```
Iteration
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        stack<TreeNode*>st;
        vector<int> ans;
        if(root==NULL) return ans;
        st.push(root);
        while(!st.empty()){
                TreeNode *cur=st.top();
                st.pop();
                ans.push_back(cur->val);
                if(cur->left)st.push(cur->left);
                if(cur->right)st.push(cur->right);
        }
            reverse(ans.begin(),ans.end());
            return ans;
    }
};
```
