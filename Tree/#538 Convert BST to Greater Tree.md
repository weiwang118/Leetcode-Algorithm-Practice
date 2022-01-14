#### #538 Convert BST to Greater Tree
[Leetcode #538](https://leetcode.com/problems/convert-bst-to-greater-tree/)  

##### My Solution
As we all know, traverse the binary search tree in inorder will get the increasing array, and so if we traverse binary search tree in reverse inorder, then we can get a drecreasing array.  The key of each node is the sum of all keys before it and itself.  
```
class Solution {
public:
    TreeNode* convertBST(TreeNode* root) {
        stack<TreeNode*>st;
        TreeNode *cur=root;
        int sum=0;
        while(cur||!st.empty()){
                if(cur){
                        st.push(cur);
                        cur=cur->right;
                }
                else{
                        cur=st.top();
                        st.pop();
                        sum+=cur->val;
                        cur->val=sum;
                        cur=cur->left;
                }
        }
            return root;
    }
};
```

##### Solution from Carl
```
class Solution {
private:
    int pre; // 记录前一个节点的数值
    void traversal(TreeNode* root) {
        stack<TreeNode*> st;
        TreeNode* cur = root;
        while (cur != NULL || !st.empty()) {
            if (cur != NULL) {
                st.push(cur);
                cur = cur->right;   // 右
            } else {
                cur = st.top();     // 中
                st.pop();
                cur->val += pre;
                pre = cur->val;
                cur = cur->left;    // 左
            }
        }
    }
public:
    TreeNode* convertBST(TreeNode* root) {
        pre = 0;
        traversal(root);
        return root;
    }
};
```
