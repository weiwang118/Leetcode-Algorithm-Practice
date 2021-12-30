#### #27 Remove Element
[Leetcode #27](https://leetcode.com/problems/remove-element/)  
###### My Solution  
```
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int n=nums.size();
        for(int i=0;i<n;i++) {
                if(nums[i]==val){
                        int j=i;
                        while(j<n-1){
                                nums[j]=nums[j+1];
                                j++;
                        }
                        n--;
                        i--;
                }
                
        }
            return n;
    }
};
```
Time Complexity: O(n^2)  
Space Complexity: O(1)  

##### Better Solution from Carl
![image](https://user-images.githubusercontent.com/93847013/147716433-dbff3e0a-3ceb-4100-b9ac-77cd5dc8acf5.png)
```
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slowIndex = 0;
        for (int fastIndex = 0; fastIndex < nums.size(); fastIndex++) {
            if (val != nums[fastIndex]) {
                nums[slowIndex++] = nums[fastIndex];
            }
        }
        return slowIndex;
    }
};
```
Time Complexity：O(n)  
Space Complexity：O(1)  
