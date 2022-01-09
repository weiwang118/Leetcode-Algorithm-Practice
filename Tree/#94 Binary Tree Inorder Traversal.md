#### #94 Binary Tree Inorder Traversal
[Leetcode #94](https://leetcode.com/problems/binary-tree-inorder-traversal/)  

##### My Solution
```
\\Recursion
class Solution {
public:
        void Traversal(TreeNode*cur, vector<int>& vec){
                if(cur==NULL) return;
                Traversal(cur->left,vec);
                vec.push_back(cur->val);
                Traversal(cur->right,vec);
        }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
         Traversal(root,ans);
         return ans;
    }
};
```

```
\\Iteration
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        stack<TreeNode*> st;
        vector<int> ans;
        TreeNode* cur=root;
        while(cur!=NULL||!st.empty()){
                if(cur!=NULL){
                        st.push(cur);
                        cur=cur->left;
                }
                else{
                        cur=st.top();
                        st.pop();
                        ans.push_back(cur->val);
                        cur=cur->right;
                        
                }
        }
            return ans;
    }
};
```
