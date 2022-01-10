#### #226 Invert Binary Tree
[Leetcode #226](https://leetcode.com/problems/invert-binary-tree/)  

##### My Solution
Breadth-First Search
```
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root==NULL) return root;
        queue<TreeNode*>que;
        que.push(root);
        while(!que.empty()){
                int size=que.size();
                for(int i=0;i<size;i++){
                        TreeNode *cur=que.front();
                        que.pop();
                        TreeNode *temp;
                        temp=cur->left;
                        cur->left=cur->right;
                        cur->right=temp;
                        //better code: swap(cur->left,cur->right);
                        if(cur->left)que.push(cur->left);
                        if(cur->right)que.push(cur->right);
                }
        }
            return root;
        
    }
};
```

Depth-First Search  
```
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
       stack<TreeNode*> st;
       if(root==NULL) return root;
         st.push(root);
          while(!st.empty()){
                  TreeNode *cur=st.top();
                  st.pop();
                  swap(cur->left,cur->right);
                  if(cur->right)st.push(cur->right);
                  if(cur->left)st.push(cur->left);
          }
            return root;
    }
};
```


