#### #509 Fibonacci Number
[Leetcode #509](https://leetcode.com/problems/fibonacci-number/)  

##### My Solution
```
class Solution {
public:
    int fib(int n) {
        if(n==0) return 0;
        vector<int> dp(n+1,0);
        dp[0]=0;
        dp[1]=1;
        for(int i=2;i<=n;i++){
                dp[i]=dp[i-1]+dp[i-2];
        }
            return dp[n];
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  

##### Solution from Carl
```
class Solution {
public:
    int fib(int N) {
        if (N <= 1) return N;
        int dp[2];
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i <= N; i++) {
            int sum = dp[0] + dp[1];
            dp[0] = dp[1];
            dp[1] = sum;
        }
        return dp[1];
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  


