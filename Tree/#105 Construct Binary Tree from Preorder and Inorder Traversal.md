#### #105 Construct Binary Tree from Preorder and Inorder Traversal
[Leetcode #105](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)  

##### My Solution
```
class Solution {
private:
    int preIdx;
    unordered_map<int,int> idxMap;
    TreeNode* Traversal(int inleft,int inright,vector<int>&preorder,vector<int>&inorder){
            if(inleft>inright) return nullptr;
            int rootvalue=preorder[preIdx];
            TreeNode *root=new TreeNode(rootvalue);
            
            int index=idxMap[rootvalue];
            preIdx++;
            root->left=Traversal(inleft,index-1,preorder,inorder);
            root->right=Traversal(index+1,inright,preorder,inorder);
            return root;
    }
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        preIdx=0;
        int idx=0;
        for(auto val:inorder)
                idxMap[val]=idx++;
        return Traversal(0,inorder.size()-1,preorder,inorder);
    }
};
```
Time Complexity:O(n)  
Space Complexity:O(n)  
