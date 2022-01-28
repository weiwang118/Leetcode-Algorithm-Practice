#### #70 Climbing Stairs
[Leetcode #70](https://leetcode.com/problems/climbing-stairs/)  

##### My Solution
```
class Solution {
public:
    int climbStairs(int n) {
        if(n<=2) return n;
        int step1=1,step2=2;
        int ans;
        for(int i=3;i<=n;i++){
                ans=step1+step2;
                step1=step2;
                step2=ans;
        }
            return ans;
        
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
