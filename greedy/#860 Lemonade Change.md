#### #860 Lemonade Change
[Leetcode #860](https://leetcode.com/problems/lemonade-change/)  

##### My Solution
```
class Solution {
public:
    bool lemonadeChange(vector<int>& bills) {
        int count5=0,count10=0;
        for(int i=0;i<bills.size();i++){
                if(bills[i]==5)
                        count5++;
                else if(bills[i]==10){
                        count5--;
                        count10++;
                }
                else if(bills[i]==20){
                        if(count10>0){
                                count10--;
                                count5--;
                        }
                        else count5=count5-3;
                }
                if(count5<0) return false;
        }
            return true;
    }
};
```
