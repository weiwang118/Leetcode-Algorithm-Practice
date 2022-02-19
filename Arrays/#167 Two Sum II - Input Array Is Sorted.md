#### #167 Two Sum II - Input Array Is Sorted
[Leetcode #167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)  

##### My Solution
```
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int slowIdx=0,fastIdx=numbers.size()-1;
        while(slowIdx<fastIdx){
                if(numbers[slowIdx]+numbers[fastIdx]==target){
                        return {slowIdx+1,fastIdx+1};
                }
                else if(numbers[slowIdx]+numbers[fastIdx]>target)
                        fastIdx--;
                else slowIdx++;
        }
            return {};
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
