#### #106 Construct Binary Tree from Inorder and Postorder Traversal
[Leetcode #106](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)  

##### My Solution
```
class Solution {
private:
    TreeNode* Traversal(vector<int>&inorder,vector<int>&postorder){
            if(postorder.size()==0)return NULL;
            int rootvalue=postorder[postorder.size()-1];
            TreeNode*root=new TreeNode(rootvalue);
            
            if(postorder.size()==1) return root;
            
            int breakval;
            for(breakval=0;breakval<inorder.size();breakval++){
                    if(inorder[breakval]==rootvalue)break;
            }
            
            vector<int> inleft(inorder.begin(),inorder.begin()+breakval);
            vector<int> inright(inorder.begin()+breakval+1,inorder.end());
            
            postorder.resize(postorder.size()-1);
            vector<int> postleft(postorder.begin(),postorder.begin()+inleft.size());
            vector<int> postright(postorder.begin()+inleft.size(),postorder.end());
            
            root->left=Traversal(inleft,postleft);
            root->right=Traversal(inright,postright);
            
            return root;
    }
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if(inorder.size()==0||postorder.size()==0) return NULL;
            return Traversal(inorder,postorder);
    }
};
```

##### Leetcode Solution
```
class Solution {
    int post_idx;
    unordered_map<int, int> idx_map;
public:
    TreeNode* helper(int in_left, int in_right, vector<int>& inorder, vector<int>& postorder){
        // 如果这里没有节点构造二叉树了，就结束
        if (in_left > in_right) {
            return nullptr;
        }

        // 选择 post_idx 位置的元素作为当前子树根节点
        int root_val = postorder[post_idx];
        TreeNode* root = new TreeNode(root_val);

        // 根据 root 所在位置分成左右两棵子树
        int index = idx_map[root_val];

        // 下标减一
        post_idx--;
        // 构造右子树
        root->right = helper(index + 1, in_right, inorder, postorder);
        // 构造左子树
        root->left = helper(in_left, index - 1, inorder, postorder);
        return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        // 从后序遍历的最后一个元素开始
        post_idx = (int)postorder.size() - 1;

        // 建立（元素，下标）键值对的哈希表
        int idx = 0;
        for (auto& val : inorder) {
            idx_map[val] = idx++;
        }
        return helper(0, (int)inorder.size() - 1, inorder, postorder);
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  
