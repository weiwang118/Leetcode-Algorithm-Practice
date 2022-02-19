#### #11 Container With Most Water
[Leetcode #11](https://leetcode.com/problems/container-with-most-water/)  

##### My Solution
```
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left=0,right=height.size()-1;
        int MaxArea=0;
        while(left<right){
                int Area=min(height[left],height[right])*(right-left);
                MaxArea=max(MaxArea,Area);
                if(height[left]<height[right])
                        left++;
                else right--;
        }
            return MaxArea;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
