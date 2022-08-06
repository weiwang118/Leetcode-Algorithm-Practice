#### #150 Evaluate Reverse Polish Notation
[Leetcode #150](https://leetcode.com/problems/evaluate-reverse-polish-notation/)  

##### My Solution
```
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;
        int num1,num2;
        for(int i=0;i<tokens.size();i++){
                if(tokens[i]=="+"){
                       num1=st.top();st.pop();
                       num2=st.top();st.pop();
                        st.push(num1+num2);
                }
                else if(tokens[i]=="-"){
                       num1=st.top();st.pop();
                       num2=st.top();st.pop();
                       st.push(num2-num1);
                }
                else if(tokens[i]=="*"){
                       num1=st.top();st.pop();
                       num2=st.top();st.pop();
                        st.push(num1*num2);
                }
                else  if(tokens[i]=="/"){
                       num1=st.top();st.pop();
                       num2=st.top();st.pop();
                        st.push(num2/num1);
                }
                else st.push(stoi(tokens[i]));
        }
            return st.top();
    }
};
```
2022.08.05  
```
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;
        for(int i = 0; i < tokens.size(); i++){
                if(tokens[i] == "+" || tokens[i] == "*" || tokens[i] == "/" || tokens[i] == "-"){
                        int n2 = st.top();
                        st.pop();
                        int n1 = st.top();
                        st.pop();
                        
                        switch(tokens[i][0]){
                                case '+': st.push(n1+n2); break;
                                case '-': st.push(n1-n2); break;
                                case '*': st.push(n1*n2); break;
                                case '/': st.push(n1/n2); break;
                        }
                }
                
                else st.push(stoi(tokens[i]));
        }
          return st.top();  
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;
        for (int i = 0; i < tokens.size(); i++) {
            if (tokens[i] == "+" || tokens[i] == "-" || tokens[i] == "*" || tokens[i] == "/") {
                int num1 = st.top();
                st.pop();
                int num2 = st.top();
                st.pop();
                if (tokens[i] == "+") st.push(num2 + num1);
                if (tokens[i] == "-") st.push(num2 - num1);
                if (tokens[i] == "*") st.push(num2 * num1);
                if (tokens[i] == "/") st.push(num2 / num1);
            } else {
                st.push(stoi(tokens[i]));
            }
        }
        int result = st.top();
        st.pop(); // 把栈里最后一个元素弹出（其实不弹出也没事）
        return result;
    }
};
```
