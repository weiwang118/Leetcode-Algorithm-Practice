#### #20 Valid Parentheses
[Leetcode #20](https://leetcode.com/problems/valid-parentheses/)  



##### My Solution
```
class Solution {
public:
    bool isValid(string s) {
            stack<int> st;
            for(int i=0;i<s.size();i++){
                    if (s[i] == '(') st.push(')');
                    else if (s[i] == '{') st.push('}');
                    else if (s[i] == '[') st.push(']');
                    else if(st.empty()||st.top()!=s[i]) return false;
                    else st.pop();
            }
            return st.empty();
    }
};
```

2022.08.04  
```
class Solution {
public:
    bool isValid(string s) {
        stack<char> In, Out;
        for(char ch:s)
                In.push(ch);
        
        while(!In.empty()){
                char pa = In.top();
                In.pop();
                if(!Out.empty()){
                  if(pa == '[' && Out.top() == ']')
                          Out.pop();
                  else if(pa == '{' && Out.top() == '}')
                          Out.pop();
                  else if(pa == '(' && Out.top() == ')')
                          Out.pop();
                  else Out.push(pa);
                }
                else if(Out.empty())
                        Out.push(pa);
        }
            return In.empty()&&Out.empty();
    }
};

```

##### Solution from Carl
```
class Solution {
public:
    bool isValid(string s) {
        stack<int> st;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(') st.push(')');
            else if (s[i] == '{') st.push('}');
            else if (s[i] == '[') st.push(']');
            // 第三种情况：遍历字符串匹配的过程中，栈已经为空了，没有匹配的字符了，说明右括号没有找到对应的左括号 return false
            // 第二种情况：遍历字符串匹配的过程中，发现栈里没有我们要匹配的字符。所以return false
            else if (st.empty() || st.top() != s[i]) return false;
            else st.pop(); // st.top() 与 s[i]相等，栈弹出元素
        }
        // 第一种情况：此时我们已经遍历完了字符串，但是栈不为空，说明有相应的左括号没有右括号来匹配，所以return false，否则就return true
        return st.empty();
    }
};
```
