# 代码随想录第24天｜回溯算法part01，理论基础，77 组合

## 回溯算法理论基础
回溯法又叫回溯搜索法，是一种搜索的方式。回溯法运行效率并不高，本质是穷举所有的可能，然后选出想要的答案。  
回溯三部曲：1. 回溯函数模板返回值和参数 void backtracking(params) 2. 回溯函数终止条件 if(终止条件){存放结果；return；} 3. 回溯搜索的遍历过程：回溯法一般在集合中递归搜索，集合的大小是树的宽度，递归的深度是树的深度。   
回溯算法代码框架如下：
```
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```
回溯算法其实就是递归中嵌套for循环

## 77 组合
用树来表示该问题，解决问题套用回溯法的模板即可，所以一定要记住该模板，遇到问题不至于毫无头绪。
```
class Solution {
private:
    vector<vector<int>> result;
    vector<int> path;
    void backtracking(int n, int k, int startIndex) {
        if (path.size() == k) {
            result.push_back(path);
            return;
        }
        for (int i = startIndex; i <= n; i++) { 
            // 该部分可以进行剪枝操作改为for (int i = startIndex; i <= n-(k-path.size())+1; i++) 因为再往后遍历没有意义了，无法满足要求。
            path.push_back(i);
            backtracking(n, k, i+1);
            path.pop_back();
        }
    }
public:
    vector<vector<int>> combine(int n, int k) {
        backtracking(n, k, 1);
        return result;
    }
};
```

