#### #454 4Sum II
[Leetcode #454](https://leetcode.com/problems/4sum-ii/)  

##### My Solution
```
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int,int> map;
        for(int n1:nums1){
                for(int n2:nums2)
                        map[n1+n2]++;
        }
        int ans=0;
        for(int n3:nums3)
        {
                for(int n4:nums4)
                {
                        if(map.find(0-(n3+n4))!=map.end())
                                ans+=map.find(0-(n3+n4))->second;
                }
        }
                return ans;
                        
    }
};
```
Time Complexity: O(n^2)  
Space Complexity: O(n^2)  

##### Solution from Carl
```
class Solution {
public:
    int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
        unordered_map<int, int> umap; //key:a+b的数值，value:a+b数值出现的次数
        // 遍历大A和大B数组，统计两个数组元素之和，和出现的次数，放到map中
        for (int a : A) {
            for (int b : B) {
                umap[a + b]++;
            }
        }
        int count = 0; // 统计a+b+c+d = 0 出现的次数
        // 在遍历大C和大D数组，找到如果 0-(c+d) 在map中出现过的话，就把map中key对应的value也就是出现次数统计出来。
        for (int c : C) {
            for (int d : D) {
                if (umap.find(0 - (c + d)) != umap.end()) {
                    count += umap[0 - (c + d)];
                }
            }
        }
        return count;
    }
};
```
Time Complexity: O(n^2)  
Space Complexity: O(n^2)  
