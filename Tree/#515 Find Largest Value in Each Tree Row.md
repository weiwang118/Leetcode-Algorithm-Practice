#### #515 Find Largest Value in Each Tree Row
[Leetcode #515](https://leetcode.com/problems/find-largest-value-in-each-tree-row/)  

##### My Solution
```
class Solution {
public:
    vector<int> largestValues(TreeNode* root) {
        vector<int> ans;
        queue<TreeNode*> que;
        if(root==NULL) return ans;
        que.push(root);
        while(!que.empty()){
                int max=INT_MIN;
                int size=que.size();
                for(int i=0;i<size;i++){
                        TreeNode*cur=que.front();
                        que.pop();
                        max=max>cur->val?max:cur->val;
                        if(cur->left)que.push(cur->left);
                        if(cur->right)que.push(cur->right);
                }
                ans.push_back(max);
        }
            return ans;
    }
};
```
