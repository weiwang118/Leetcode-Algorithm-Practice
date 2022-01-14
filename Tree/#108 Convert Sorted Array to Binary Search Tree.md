##### #108 Convert Sorted Array to Binary Search Tree
[Leetcode #108](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)  

##### My Solution
```
class Solution {
private:
     TreeNode* BST(vector<int>&nums,int left,int right){
        if(left>right) return nullptr;
        int i=(left+right)/2;
        TreeNode *root=new TreeNode(nums[i]);
        root->left=BST(nums,left,i-1);
        root->right=BST(nums,i+1,right);
        return root;
}
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        if(nums.size()==0) return nullptr;
            return BST(nums,0,nums.size()-1);
    }
};
```
The interval is [left,right], so when left=right, it is still valid, but when left>right, it's nullptr;  

##### Solution from Carl
Iteration  
```
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        if (nums.size() == 0) return nullptr;

        TreeNode* root = new TreeNode(0);   // 初始根节点
        queue<TreeNode*> nodeQue;           // 放遍历的节点
        queue<int> leftQue;                 // 保存左区间下标
        queue<int> rightQue;                // 保存右区间下标
        nodeQue.push(root);                 // 根节点入队列
        leftQue.push(0);                    // 0为左区间下标初始位置
        rightQue.push(nums.size() - 1);     // nums.size() - 1为右区间下标初始位置

        while (!nodeQue.empty()) {
            TreeNode* curNode = nodeQue.front();
            nodeQue.pop();
            int left = leftQue.front(); leftQue.pop();
            int right = rightQue.front(); rightQue.pop();
            int mid = left + ((right - left) / 2);

            curNode->val = nums[mid];       // 将mid对应的元素给中间节点

            if (left <= mid - 1) {          // 处理左区间
                curNode->left = new TreeNode(0);
                nodeQue.push(curNode->left);
                leftQue.push(left);
                rightQue.push(mid - 1);
            }

            if (right >= mid + 1) {         // 处理右区间
                curNode->right = new TreeNode(0);
                nodeQue.push(curNode->right);
                leftQue.push(mid + 1);
                rightQue.push(right);
            }
        }
        return root;
    }
};
```
