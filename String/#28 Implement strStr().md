#### #28 Implement strStr()
[Leetcode #28](https://leetcode.com/problems/implement-strstr/)  

##### My Solution
```
class Solution {
public:
    int strStr(string haystack, string needle) {
        return haystack.find(needle);
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    void getNext(int*next,const string&s){
            int j=0;
            next[0]=0;
            for(int i=1;i<s.size();i++){
                    while(j>0 && s[i]!=s[j]){
                            j=next[j-1];
                    }
                    
                    if(s[j]==s[i])
                            j++;
                    next[i]=j;
            }
    }
    int strStr(string haystack, string needle) {
        if(needle.size()==0) return 0;
        int next[needle.size()];
        getNext(next,needle);
        int j=0;
        for(int i=0;i<haystack.size();i++){
                while( j>0 && haystack[i]!=needle[j]){
                        j=next[j-1];
                }
                if(haystack[i]==needle[j])
                        j++;
                if(j==needle.size())
                        return (i-needle.size()+1);
        }
            return -1;
    }
};
```

##### Notes
KMP algorithm is often used to match substring in a string with time complexity O(m+n).  
[Carl explanation](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0028.%E5%AE%9E%E7%8E%B0strStr.md)  
