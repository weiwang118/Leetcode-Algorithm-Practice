#### #455 Assign Cookies
[Leetcode #455](https://leetcode.com/problems/assign-cookies/)  

##### My Solution
```
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        if(s.size()==0||g.size()==0) return 0;
        sort(g.begin(),g.end());
        sort(s.begin(),s.end());
        int i=0;
        for(int j=0;j<s.size();j++){
                if(i<g.size()&&s[j]>=g[i]) i++;
        }
            return i;
    }
};
```
Time Complexity: O(nlogn)  
Space Complexity: O(1)  

##### Solution from Carl
```
// 时间复杂度：O(nlogn)
// 空间复杂度：O(1)
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        int index = s.size() - 1; // 饼干数组的下标
        int result = 0;
        for (int i = g.size() - 1; i >= 0; i--) {
            if (index >= 0 && s[index] >= g[i]) {
                result++;
                index--;
            }
        }
        return result;
    }
};
```
