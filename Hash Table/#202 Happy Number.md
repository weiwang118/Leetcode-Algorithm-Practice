#### #202 Happy Number
[Leetcode #202](https://leetcode.com/problems/happy-number/)  
##### My Solution
```
class Solution {
public:
    int getSum(int n){
            int sum=0;
            while(n){
                    sum+=(n%10)*(n%10);
                    n/=10;
            }
            return sum;
    }
        
    bool isHappy(int n) {
        unordered_set <int> set;
        while(1){
                int sum=getSum(n);
                if(sum==1)return true;
                if(set.find(sum)!=set.end())
                        return false;
                else{
                        set.insert(sum);
                }
                n=sum;
        }
    }
};
```
##### Notes
The key to the question is that if the sum repeats, it means it loops endlessly in a circle. As we all know, unordered_set is quite efficient to lookup an element, so we insert the sum to the set and check if the following sum repeats.  
