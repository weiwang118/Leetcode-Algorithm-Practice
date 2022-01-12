#### #98 Validate Binary Search Tree
[Leetcode #98](https://leetcode.com/problems/validate-binary-search-tree/)  

##### My Solution
Inorder Traverse binary search tree, then you can get a increasing ordered array.  
```
class Solution {
private:
        vector<int> vec;
        void Traversal(TreeNode*root){
                if(root==NULL) return;
                Traversal(root->left);
                vec.push_back(root->val);
                Traversal(root->right);
        }
public:
    bool isValidBST(TreeNode* root) {
            Traversal(root);
            for(int i=0;i<vec.size()-1;i++){
                    if(vec[i]>=vec[i+1]) return false;
            }
            return true;
    }
};
```
Inorder Traversal Recursion  
```
class Solution {
public:
    TreeNode *pre=NULL;
    bool isValidBST(TreeNode* root) {
           if(root==NULL) return true;
           bool left=isValidBST(root->left);
           
           if(pre!=NULL&&pre->val>=root->val) return false;
            pre=root;
            
            bool right=isValidBST(root->right);
            return left&&right;
            
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  

Inorder Traversal Iteration  
```
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        stack<TreeNode*> st;
        TreeNode* cur = root;
        TreeNode* pre = NULL; // 记录前一个节点
        while (cur != NULL || !st.empty()) {
            if (cur != NULL) {
                st.push(cur);
                cur = cur->left;                // 左
            } else {
                cur = st.top();                 // 中
                st.pop();
                if (pre != NULL && cur->val <= pre->val)
                return false;
                pre = cur; //保存前一个访问的结点

                cur = cur->right;               // 右
            }
        }
        return true;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  
