# 代码随想录第10天｜ 232.用栈实现队列 225. 用队列实现栈

## 232 用栈实现队列
该问题用stack实现queue，需要区分进栈和出栈，用两个栈实现队列的功能。

```
class MyQueue {
public:
    stack<int> stackIn;
    stack<int> stackOut; 
    MyQueue() {
        
    }
    
    void push(int x) {
        stackIn.push(x);
    }
    
    int pop() {
        if (stackOut.empty()) {
            while (!stackIn.empty()) {
                stackOut.push(stackIn.top());
                stackIn.pop();
            }
        }
        int res = stackOut.top();
        stackOut.pop();
        return res;
    }
    
    int peek() {
        int res = this->pop();
        stackOut.push(res);
        return res;
    }
    
    bool empty() {
        return stackIn.empty() && stackOut.empty();
    }
};
```

## 225 用队列实现栈