#### #257 Binary Tree Paths
[Leetcode #257](https://leetcode.com/problems/binary-tree-paths/)  

![257.二叉树的所有路径](https://img-blog.csdnimg.cn/20210204151702443.png)

##### My Solution
Recursion  
```
class Solution {
private:
    void Traversal(TreeNode *cur,string path,vector<string>& result){
            path+=to_string(cur->val);
            if(!cur->left&&!cur->right){
                    result.push_back(path);
                    return;
            }
            if(cur->left) Traversal(cur->left,path+"->",result);
            if(cur->right) Traversal(cur->right,path+"->",result);
            
    }
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> result;
        string path;
         if(root==NULL) return result;
         Traversal(root,path,result);
            return result;
    }
};
```

Iteration  
```
class Solution {
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> result;
        stack<string> path;
        stack<TreeNode*> st;
        if(root==NULL) return result;
        st.push(root);
        path.push(to_string(root->val));
        while(!st.empty()){
                TreeNode *cur=st.top();st.pop();
                string spath=path.top();path.pop();
                if(!cur->left&&!cur->right){
                        result.push_back(spath);
                }
                if(cur->right){
                        st.push(cur->right);
                        path.push(spath+"->"+to_string(cur->right->val));
                }
                if(cur->left){
                        st.push(cur->left);
                        path.push(spath+"->"+to_string(cur->left->val));
        }
    }
            return result;}
};
```
