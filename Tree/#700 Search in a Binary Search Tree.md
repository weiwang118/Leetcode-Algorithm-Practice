#### #700 Search in a Binary Search Tree
[Leetcode #700](https://leetcode.com/problems/search-in-a-binary-search-tree/)  

##### My Solution
Recursion
```
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        if(root==NULL) return NULL;
        if(root->val==val) return root;
        else if(root->val>val) root=searchBST(root->left,val);
        else root=searchBST(root->right,val);
        return root;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  
Because in the worst situation, the binary search tree may be like a linked list where it need O(n) time to traverse all the nodes and don't find the equal value.  
As it may need O(n) recursions, it causes O(n) stack space for the recursions.  


Iteration
```
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        stack<TreeNode*> st;
        if(root!=NULL) st.push(root);
        while(!st.empty()){
                TreeNode *cur=st.top();st.pop();
                if(cur->val==val) return cur;
                if(cur->val>val) {if(cur->left)st.push(cur->left);}
                else{if(cur->right) st.push(cur->right);}
        }
            return NULL;
    }
};
```
Actually, there is no need to use stack. Although stack is often used to simulate depth-first search for binary tree, binary search tree is ordered which means it doesn't need stack to simualte the search.  

Iteration without stack
```
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        while(root){
                if(root->val==val) return root;
                else if(root->val>val) root=root->left;
                else root=root->right;
        }
            return nullptr;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
