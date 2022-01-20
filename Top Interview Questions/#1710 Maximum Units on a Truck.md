#### #1710 Maximum Units on a Truck
[Leetcode #1710](https://leetcode.com/problems/maximum-units-on-a-truck/)  

##### My Solution
```
class Solution {
public:
    static bool cmp(const vector<int> &b1,const vector<int> &b2){
            return b1[1]>b2[1];
    }
    int maximumUnits(vector<vector<int>>& boxTypes, int truckSize) {
        sort(boxTypes.begin(),boxTypes.end(),cmp);
        int sum=0;
        for(int i=0;i<boxTypes.size();i++){
              int boxCount=min(truckSize,boxTypes[i][0]);
                sum+=boxCount*boxTypes[i][1];
                truckSize-=boxCount;
                if(truckSize==0) break;
        }
            return sum;
    }
};
```
Time Complexity: O(nlogn)  
Space Complexity: O(1)  
