#### #501 Find Mode in Binary Search Tree
[Leetcode #501](https://leetcode.com/problems/find-mode-in-binary-search-tree/)  

##### My Solution
First, if this is just a binary tree instead of a binary search tree, we can use unordered_map to store all the values and their frequency. But due to the data structure of map, we can only sort key of map, not the value, so convert map to vector and then sort the vector by increasing order.  The biggest elements in the vector is what we want.  
```
class Solution {
public:
    void searchBST(TreeNode*cur,unordered_map<int,int>&map){
            if(cur==NULL) return;
            map[cur->val]++;
            searchBST(cur->left,map);
            searchBST(cur->right,map);
            return;
    }
    bool static cmp(const pair<int,int>&a,const pair<int,int>&b){
            return a.second>b.second;
    }
    vector<int> findMode(TreeNode* root) {
        unordered_map<int,int>map;
        searchBST(root,map);
        vector<int>result;
        if(root==NULL) return result;
        vector<pair<int,int>> vec(map.begin(),map.end());
        sort(vec.begin(),vec.end(),cmp);
        result.push_back(vec[0].first);
        for(int i=1;i<vec.size();i++){

                if(vec[i].second==vec[0].second)   result.push_back(vec[i].first);
                else break;
        }
            return result;
    }
};
```

There is another way that uses the nature of binary search tree.  
Recursion  
```
class Solution {
private:
    int maxCount;
    int count;
    TreeNode *pre;
    vector<int>ans;
public:
    void searchBST(TreeNode *cur){
            if(cur==NULL) return;
            searchBST(cur->left);
            if(pre==NULL) count=1;
            else if(pre->val==cur->val){
                    count++;
            }
            else count=1;
            pre=cur;
            if(count==maxCount)
                    ans.push_back(cur->val);
            else if(count>maxCount){
                    maxCount=count;
                    ans.clear();
                    ans.push_back(cur->val);
            }
            searchBST(cur->right);
            return;
    }
    vector<int> findMode(TreeNode* root) {
        maxCount=0;
        count=0;
        pre=NULL;
        searchBST(root);
           return ans;
    }
};
```

Iteration  
```
class Solution {
public:
    vector<int> findMode(TreeNode* root) {
        int maxCount=0;
        int count=0;
        TreeNode *pre=NULL;
        TreeNode *cur=root;
        vector<int> ans;
        stack<TreeNode*> st;
        while(cur||!st.empty()){
                if(cur){
                        st.push(cur);
                        cur=cur->left;
                }
                else{
                        cur=st.top();
                        st.pop();
                        if(pre==NULL) count=1;
                        else if(pre->val==cur->val)count++;
                        else count=1;
                        pre=cur;
                        if(count==maxCount){
                                ans.push_back(cur->val);
                        }
                        if(count>maxCount){
                                maxCount=count;
                                ans.clear();
                                ans.push_back(cur->val);
                        }
                        cur=cur->right;
                }
                
        }
            return ans;
      
    }
};
```



