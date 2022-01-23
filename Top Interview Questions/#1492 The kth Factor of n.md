#### #1492 The kth Factor of n
[Leetcode #1492](#1492 The kth Factor of n)  

##### My Solution
```
class Solution {
public:
    int kthFactor(int n, int k) {
        for(int i=1;i<=n;i++){
                if(n%i==0) k--;
                if(k==0) return i;
        }
            return -1;
    }
};
```
Time complexity: O(n)  
Space Complexity: O(1)  

##### Leetcode Solution
```
class Solution {
public:
    int kthFactor(int n, int k) {
        int count = 0, factor;
        for (factor = 1; factor * factor <= n; ++factor) {
            if (n % factor == 0) {
                ++count;
                if (count == k) {
                    return factor;
                }
            }
        }
        --factor;
        if (factor * factor == n) {
            --factor;
        }
        for (; factor > 0; --factor) {
            if (n % factor == 0) {
                ++count;
                if (count == k) {
                    return n / factor;
                }
            }
        }
        return -1;
    }
};
```
Time Complexity: O(sqrt(n))  
Space Complexity: O(1)  
