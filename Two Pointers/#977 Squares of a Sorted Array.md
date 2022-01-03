#### #977 Squares of a Sorted Array
[Leetcode #977](https://leetcode.com/problems/squares-of-a-sorted-array/)  
##### My Solution
```
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int slowindex=0;
        int fastindex=nums.size()-1;
        vector<int> newarray(nums.size());
        for(int i=nums.size()-1;i>=0;i--){
                int num1=nums[fastindex]*nums[fastindex];
                int num2=nums[slowindex]*nums[slowindex];
                if(num1<num2)
                {
                        newarray[i]=num2;
                        slowindex++;
                }
                else {newarray[i]=num1;
                      fastindex--;}
                
        }
            return newarray;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  

##### Solution From Carl
```
class Solution {
public:
    vector<int> sortedSquares(vector<int>& A) {
        int k = A.size() - 1;
        vector<int> result(A.size(), 0);
        for (int i = 0, j = A.size() - 1; i <= j;) { // 注意这里要i <= j，因为最后要处理两个元素
            if (A[i] * A[i] < A[j] * A[j])  {
                result[k--] = A[j] * A[j];
                j--;
            }
            else {
                result[k--] = A[i] * A[i];
                i++;
            }
        }
        return result;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  
