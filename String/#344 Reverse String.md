#### #344 Reverse String
[Leetcode #344](https://leetcode.com/problems/reverse-string/)  

##### My Solution
```
class Solution {
public:
    void reverseString(vector<char>& s) {
        reverse(s.begin(),s.end());
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    void reverseString(vector<char>& s) {
        for (int i = 0, j = s.size() - 1; i < s.size()/2; i++, j--) {
            swap(s[i],s[j]);
        }
    }
};
```

##### Notes:
Although there are many functions in string's library, don't always use them to solve leetcode problem.  
