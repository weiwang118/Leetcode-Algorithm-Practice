#### #452 Minimum Number of Arrows to Burst Balloons
[Leetcode #452](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/)  

##### My Solution
```
class Solution {
public:
    int findMinArrowShots(vector<vector<int>>& points) {
       sort(points.begin(),points.end());
       int arrows=1;
       long left=points[0][0],right=points[0][1];
        for(int i=1;i<points.size();i++){
                if(points[i][0]<=right)
                {
                        left=points[i][0];
                        right=points[i][1]<right?points[i][1]:right;
                }
                else {
                        arrows++;
                        left=points[i][0];
                        right=points[i][1];
                }
        }
            return arrows;
    }
};
```
Time Complexity: O(nlogn)  
Space Complexity: O(1)  

##### Solution from Carl
```
class Solution {
private:
    static bool cmp(const vector<int>& a, const vector<int>& b) {
        return a[0] < b[0];
    }
public:
    int findMinArrowShots(vector<vector<int>>& points) {
        if (points.size() == 0) return 0;
        sort(points.begin(), points.end(), cmp);

        int result = 1; // points 不为空至少需要一支箭
        for (int i = 1; i < points.size(); i++) {
            if (points[i][0] > points[i - 1][1]) {  // 气球i和气球i-1不挨着，注意这里不是>=
                result++; // 需要一支箭
            }
            else {  // 气球i和气球i-1挨着
                points[i][1] = min(points[i - 1][1], points[i][1]); // 更新重叠气球最小右边界
            }
        }
        return result;
    }
};
```
Time Complexity: O(nlogn)  
Space Complexity: O(1)  
