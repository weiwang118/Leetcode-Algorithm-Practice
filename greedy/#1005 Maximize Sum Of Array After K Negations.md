#### #1005 Maximize Sum Of Array After K Negations
[Leetcode #1005](https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/)  

##### My Solution
```
class Solution {
public:
    int largestSumAfterKNegations(vector<int>& nums, int k) {
        sort(nums.begin(),nums.end());
        int ans=0;
        int i=0;
        while(k--){
                if(nums[i]<0)
                       nums[i]*=-1; 
                 else if(nums[i]==0) 
                         break;
                 else if(nums[i]>0){
                         sort(nums.begin(),nums.end());
                         if(k%2==0) nums[0]*=-1;
                         break;
                 }
                i++;
                 if(i>=nums.size()){
                         sort(nums.begin(),nums.end());
                         i=0;
                 }
        }
        for( int i=0;i<nums.size();i++)
                ans+=nums[i];
        return ans;
            
    }
};
```

##### Solution from Carl
```
class Solution {
static bool cmp(int a, int b) {
    return abs(a) > abs(b);
}
public:
    int largestSumAfterKNegations(vector<int>& A, int K) {
        sort(A.begin(), A.end(), cmp);       // 第一步
        for (int i = 0; i < A.size(); i++) { // 第二步
            if (A[i] < 0 && K > 0) {
                A[i] *= -1;
                K--;
            }
        }
        if (K % 2 == 1) A[A.size() - 1] *= -1; // 第三步
        int result = 0;
        for (int a : A) result += a;        // 第四步
        return result;
    }
};
```
