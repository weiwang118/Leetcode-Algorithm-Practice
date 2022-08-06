#### #1047 Remove All Adjacent Duplicates In String
[Leetcode #1047](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)  

##### My Solution
```
class Solution {
public:
    string removeDuplicates(string s) {
        stack<int> st;
        for(int i=0;i<s.size();i++){
                if(!st.empty()&&st.top()==s[i]){
                        st.pop();
                }
                else st.push(s[i]);
        }
        stack<int>temp;
        while(!st.empty()){
                temp.push(st.top());
                st.pop();
        }
        s.clear();
        while(!temp.empty()){
                s+=temp.top();
                temp.pop();
        }
            return s;
    }
};
```

2022.08.05  
```
class Solution {
public:
    string removeDuplicates(string s) {
        stack<char> st;
        for(char ch:s){
                if(st.empty()||st.top()!=ch)
                        st.push(ch);
                else st.pop();
        }
        string str(st.size(),'0');
        for(int i = str.size()-1; i>=0; i--){
                str[i] = st.top();
                st.pop();
        }
            return str;
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    string removeDuplicates(string S) {
        string result;
        for(char s : S) {
            if(result.empty() || result.back() != s) {
                result.push_back(s);
            }
            else {
                result.pop_back();
            }
        }
        return result;
    }
};
```
