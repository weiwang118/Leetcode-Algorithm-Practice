#### #429 N-ary Tree Level Order Traversal
[Leetcode #429](https://leetcode.com/problems/n-ary-tree-level-order-traversal/)  

##### My Solution
```
class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        vector<vector<int>> ans;
        queue<Node*> que;
        if(root==NULL) return ans;
        que.push(root);
        while(!que.empty()){
                int size=que.size();
                vector<int> vec;
                for(int i=0;i<size;i++){
                        Node*cur=que.front();
                        que.pop();
                        vec.push_back(cur->val);
                        for(int j=0;j<cur->children.size();j++){
                                if(cur->children[j])
                                que.push(cur->children[j]);
                        }
                        
                }
                ans.push_back(vec);
                
        }
            return ans;
    }
};
```
