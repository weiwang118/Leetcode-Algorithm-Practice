#### #102 Binary Tree Level Order Traversal
[Leetcode #102](https://leetcode.com/problems/binary-tree-level-order-traversal/)  

##### My Solution
```
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        queue<TreeNode*> deq;
        vector<vector<int>> ans;
        if(root != NULL)  deq.push(root);
        while(!deq.empty()){
                int size=deq.size();
                vector<int> vec;
                for(int i=0;i<size;i++){
                        TreeNode* Node=deq.front();
                        deq.pop();
                        vec.push_back(Node->val);
                        if(Node->left)deq.push(Node->left);
                        if(Node->right)deq.push(Node->right);
                }
                ans.push_back(vec);
        }
            return ans;
    }
};
```
##### Notes
Stack is first-in-last-out, so it fits depth first search, but queue is first-in-first-out, so it fits width first search.  
