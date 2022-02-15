#### #27 Remove Element
[Leetcode #27](https://leetcode.com/problems/remove-element/)  
###### My Solution  
![27.移除元素-暴力解法](https://tva1.sinaimg.cn/large/008eGmZEly1gntrc7x9tjg30du09m1ky.gif)
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
![27.移除元素-双指针法](https://tva1.sinaimg.cn/large/008eGmZEly1gntrds6r59g30du09mnpd.gif)
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

##### Java Solution
```
class Solution {
    public int removeElement(int[] nums, int val) {
        int slowIdx=0;
        for(int fastIdx=0;fastIdx<=nums.length-1;fastIdx++){
                if(nums[fastIdx]!=val){
                        nums[slowIdx++]=nums[fastIdx];
                }
        }
            return slowIdx;
            
    }
}
```
