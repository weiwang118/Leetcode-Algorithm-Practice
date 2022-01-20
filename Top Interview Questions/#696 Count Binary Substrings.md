#### #696 Count Binary Substrings
[Leetcode 696](https://leetcode.com/problems/count-binary-substrings/)  

##### Leetcode Solution
#Approach 1 group by characters  
```
class Solution {
public:
    int countBinarySubstrings(string s) {
        int groups[s.length()],t=0;
        groups[0]=1;
        for(int i=1;i<s.length();i++){
                if(s[i-1]!=s[i])
                        groups[++t]=1;
                else
                        groups[t]++;
        }
        int ans=0;
        for(int i=1;i<=t;i++){
                ans+=min(groups[i-1],groups[i]);
        }
            return ans;
            
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(n)  

#Approach 2 Linear scan  
```
class Solution {
public:
    int countBinarySubstrings(string s) {
        int pre=0,cur=1,ans=0;
        for(int i=1;i<s.length();i++){
                if(s[i-1]!=s[i]){
                      ans+=min(pre,cur);  
                        pre=cur;
                        cur=1;
                }
                else
                        cur++;
        }
       
          return ans+min(pre,cur);  
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  

##### Notes:
When there are only two contiguous elements in the array being used, we can use two pointers instead where one is pre pointer and the other is cur pointer.  
