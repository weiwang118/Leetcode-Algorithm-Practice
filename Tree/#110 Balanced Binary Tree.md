#### #110 Balanced Binary Tree
[Leetcode #110](https://leetcode.com/problems/balanced-binary-tree/)  

##### My Solution
```
class Solution {
public:
    int Getheight(TreeNode *cur){
           if(cur== NULL) return 0;
           int Lheight=Getheight(cur->left);
           if(Lheight==-1) return -1;
           int Rheight=Getheight(cur->right);
           if(Rheight==-1) return -1;
           return abs(Lheight-Rheight)>1?-1:1+max(Lheight,Rheight);
            
    }
        
    bool isBalanced(TreeNode* root) {
            return Getheight(root)==-1?false:true;
    }
};
```
