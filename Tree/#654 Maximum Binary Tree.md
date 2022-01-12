#### #654 Maximum Binary Tree
[Leetcode #654](https://leetcode.com/problems/maximum-binary-tree/)  

##### My Solution
```
class Solution {
private:
    TreeNode* Traversal(vector<int>&nums,int left,int right){
            if(left>=right) return nullptr;
int rootvalue=*max_element(nums.begin()+left,nums.begin()+right);
int rootindex=max_element(nums.begin()+left,nums.begin()+right)-nums.begin();
            
            TreeNode *root=new TreeNode(rootvalue);
            root->left=Traversal(nums,left,rootindex);
            root->right=Traversal(nums,rootindex+1,right);
            return root;
    }
public:
    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        return Traversal(nums,0,nums.size());
    }
};
```

##### Solution from Carl
```
class Solution {
private:
    // 在左闭右开区间[left, right)，构造二叉树
    TreeNode* traversal(vector<int>& nums, int left, int right) {
        if (left >= right) return nullptr;

        // 分割点下标：maxValueIndex
        int maxValueIndex = left;
        for (int i = left + 1; i < right; ++i) {
            if (nums[i] > nums[maxValueIndex]) maxValueIndex = i;
        }

        TreeNode* root = new TreeNode(nums[maxValueIndex]);

        // 左闭右开：[left, maxValueIndex)
        root->left = traversal(nums, left, maxValueIndex);

        // 左闭右开：[maxValueIndex + 1, right)
        root->right = traversal(nums, maxValueIndex + 1, right);

        return root;
    }
public:
    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        return traversal(nums, 0, nums.size());
    }
};
```

##### Notes
Don't create new array, just create boundaries (left and right) that can apply to the original array.  



