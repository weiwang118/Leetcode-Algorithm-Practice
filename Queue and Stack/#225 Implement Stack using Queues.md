#### #225 Implement Stack using Queues
[Leetcode #225](https://leetcode.com/problems/implement-stack-using-queues/)  
##### My Solution
```
class MyStack {
public:
    queue<int> In;
    queue<int> Out;
    MyStack() {
        
    }
    
    void push(int x) {
        In.push(x);
    }
    
    int pop() {
        while(In.size()>1){
                Out.push(In.front());
                In.pop();
        }
        int val=In.front();
            In.pop();
        while(!Out.empty()){
                In.push(Out.front());
                Out.pop();
        }
            return val;
    }
    
    int top() {
        int val=this->pop();
        In.push(val);
        return val;
    }
    
    bool empty() {
        return In.empty()&&Out.empty();
    }
};
```

##### Solution from Carl
```
class MyStack {
public:
    queue<int> que;
    /** Initialize your data structure here. */
    MyStack() {

    }
    /** Push element x onto stack. */
    void push(int x) {
        que.push(x);
    }
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        int size = que.size();
        size--;
        while (size--) { // 将队列头部的元素（除了最后一个元素外） 重新添加到队列尾部
            que.push(que.front());
            que.pop();
        }
        int result = que.front(); // 此时弹出的元素顺序就是栈的顺序了
        que.pop();
        return result;
    }

    /** Get the top element. */
    int top() {
        return que.back();
    }

    /** Returns whether the stack is empty. */
    bool empty() {
        return que.empty();
    }
};
```
