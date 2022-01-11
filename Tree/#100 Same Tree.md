#### #100 Same Tree
[Leetcode #100](https://leetcode.com/problems/same-tree/)  

##### My Solution
Recursion
```
class Solution {
public:
    bool isSame(TreeNode *p, TreeNode *q){
            if(!p&&q)return false;
            else if(p&&!q)return false;
            else if(!p&&!q)return true;
            else if(p->val!=q->val) return false;
            return isSame(p->left,q->left)&&isSame(p->right,q->right);
    }
    bool isSameTree(TreeNode* p, TreeNode* q) {
            return isSame(p,q);
    }
};
```
Iteration
```
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
            queue<TreeNode*> que;
            if(!q&&!p)return true;
            que.push(p);
            que.push(q);
            while(!que.empty()){
                            TreeNode *Tree1=que.front();que.pop();
                            TreeNode *Tree2=que.front();que.pop();
                            if(!Tree1&&!Tree2)
                                    continue;
                            if(!Tree1||!Tree2||Tree1->val!=Tree2->val)
                                    return false;
                                    que.push(Tree1->left);
                                    que.push(Tree2->left);
                                    que.push(Tree1->right);
                                    que.push(Tree2->right);
            }
            return true;
    }
};
```
