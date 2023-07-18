# 代码随想录第13天｜239. 滑动窗口最大值 347.前 K 个高频元素

## 239 滑动窗口最大值
优先级队列不能使用，什么是优先级队列？

该问题可以通过维护单调队列来进行求解，基于deque，将滑动窗口中的最大值放在front。但要注意，该队列只能用于这一个题，其他题目的单调队列需要根据实际情况适配。
```
class Solution {
private:
    class MyQueue {
        public:
        deque<int> que;
        void pop(int val) {
            if (!que.empty() && val == que.front()) {
                que.pop_front();
            }
        }
        void push(int val) {
            while (!que.empty() && que.back() < val) {
                que.pop_back();
            }
            que.push_back(val);
        }
        int front() {
            return que.front();
        }
    };
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        MyQueue myqueue;
        vector<int> result;
        for (int i = 0; i < k; i++) {
            myqueue.push(nums[i]);
        }
        result.push_back(myqueue.front());
        for (int i = k; i < nums.size(); i++) {
            myqueue.pop(nums[i-k]);
            myqueue.push(nums[i]);
            result.push_back(myqueue.front());
        }
        return result;
    }
};
```

## 347 前K个高频元素
该问题需要继续学习和注意的内容如下：
1. 优先级队列 priority_queue<>;
2. 仿函数和lambda表达式；
3. unordered_map<>使用方法
```
class Solution {
public:
    class cmp {
    public:
        bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) {
            return lhs.second > rhs.second;
        }
    };
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> map;
        for (int i = 0; i < nums.size(); i++) {
            map[nums[i]]++;
        }
        priority_queue<pair<int, int>, vector<pair<int, int>>, cmp> myque;
        for (unordered_map<int, int>::iterator it = map.begin(); it != map.end(); it++) {
            myque.push(*it);
            if (myque.size() > k) {
                myque.pop();
            }
        }
        vector<int> result(k);
        for (int i = 0; i < k; i++) {
            result[i] = myque.top().first;
            myque.pop();
        }
        return result;
    }
};
```