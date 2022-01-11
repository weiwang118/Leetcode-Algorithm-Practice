#### #222 Count Complete Tree Nodes
[Leetcoed #222](https://leetcode.com/problems/count-complete-tree-nodes/)  

##### My Solution
Iteration
```
class Solution {
public:
    int countNodes(TreeNode* root) {
        if(root==NULL) return 0;
        queue<TreeNode*> que;
        que.push(root);
        int count=0;
        while(!que.empty()){
                int size=que.size();
                for(int i=0;i<size;i++){
                        TreeNode *cur=que.front();
                        que.pop();
                        if(cur->left) que.push(cur->left);
                        if(cur->right) que.push(cur->right);
                }
                count+=size;
        }
            return count;
    }
};
```

Recursion
```
class Solution {
public:
    int getcount(TreeNode *Node){
            if(Node==NULL) return 0;
            return getcount(Node->left)+getcount(Node->right)+1;
    }
    int countNodes(TreeNode* root) {
       return getcount(root);
    }
};
```


