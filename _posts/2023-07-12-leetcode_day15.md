# 代码随想录第15天｜层序遍历10 226.翻转二叉树 101.对称二叉树2  
## 层序遍历10  
层序遍历是广度优先遍历，和之前的前中后序的深度优先遍历不同，可以用队列先进后出的特性来模拟层序遍历。代码如下：

关键是使用队列来存储每一层的节点，每个for循环都代表一层的遍历，非常清晰。
```
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        queue<TreeNode*> que;
        if (root != nullptr) que.push(root);
        while (!que.empty()) {
            int size = que.size();
            vector<int> vec;
            for (int i = 0; i < size; i++) {
                TreeNode* node = que.front();
                que.pop();
                vec.push_back(node->val);
                if (node->left) que.push(node->left);
                if (node->right) que.push(node->right);
            }
            result.push_back(vec);
        }
        return result;
    }
};
```
迭代法
```
class Solution {
public:
    void order(TreeNode* node, vector<vector<int>>& result, int depth) {
        if (node == nullptr) return;
        if (result.size() == depth) result.push_back(vector<int>());
        result[depth].push_back(node->val);
        order(node->left, result, depth + 1);
        order(node->right, result, depth + 1);
    }
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        int depth = 0;
        order(root, result, depth);
        return result;
    }
};
```

## 226 翻转二叉树

## 101 对称二叉树2

