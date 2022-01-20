#### #56 Merge Intervals
[Leetcode #56](https://leetcode.com/problems/merge-intervals/)  

#### My Solution
```
class Solution {
public:
    static bool cmp(const vector<int> &n1,const vector<int> &n2){
            return n1[0]<n2[0];
    }
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(),intervals.end(),cmp);
        vector<vector<int>> ans;
        ans.push_back(intervals[0]);
        for(int i=1;i<intervals.size();i++){
              vector<int> back=ans.back();
                if(back[1]<intervals[i][0])
                        ans.push_back(intervals[i]);
                else{
                    ans.pop_back();
                        ans.push_back({back[0],max(intervals[i][1],back[1])});
                }
        }
            return ans;
    }
};
```
Time Complexity: O(nlogn)  
Space Complexity: O(n)  
