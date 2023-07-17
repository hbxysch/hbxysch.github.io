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

该问题用queue1作为主要容器，用queue作为备份即可实现栈。需要注意处理pop时候的从queue1到queue2或者反过来数据转移细节。

```
class MyStack {
public:
    queue<int> que1;
    queue<int> que2;
    MyStack() {
        
    }
    
    void push(int x) {
        que1.push(x);
    }
    
    int pop() {
        int que_size = que1.size();
        que_size--;
        while (que_size--) {
            que2.push(que1.front());
            que1.pop();
        }

        int res = que1.front();
        while (!que2.empty()) {
            que1.push(que2.front());
            que2.pop();
        }
        que1.pop();
        return res;
    }
    
    int top() {
        return que1.back();
    }
    
    bool empty() {
        return que1.empty();
    }
};
```