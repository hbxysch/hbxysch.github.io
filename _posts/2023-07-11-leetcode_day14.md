# 代码随想录第14天｜理论基础 递归遍历 迭代遍历 统一迭代
今天是二叉树相关的基础知识
## 理论基础
之前没有系统学习过二叉树，现在学习很有收获，但是仍需要持续积累，概念理解但是仍然不清楚实现过程。

## 递归遍历
递归遍历一定要注意以下三点：
1. 确定递归函数的参数和返回值
2. 确定终止条件，否则会导致栈溢出
3. 确定单层递归的逻辑

### 144 Binary Tree Preorder Travesal
前序遍历递归
```
class Solution {
public:
    void traversal (TreeNode* cur, vector<int>& ret) {
        if (cur == nullptr) return;
        ret.push_back(cur->val);
        traversal(cur->left, ret);
        traversal(cur->right, ret);
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        traversal(root, result);
        return result;
    }
};
```
后序遍历递归
```
class Solution {
public:
    void traversal (TreeNode* cur, vector<int>& ret) {
        if (cur == nullptr) return;
        traversal(cur->left, ret);
        traversal(cur->right, ret);
        ret.push_back(cur->val);
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> result;
        traversal(root, result);
        return result;
    }
};
```
中序遍历
```
class Solution {
public:
    void traversal (TreeNode* cur, vector<int>& ret) {
        if (cur == nullptr) return;
        traversal(cur->left, ret);
        ret.push_back(cur->val);
        traversal(cur->right, ret);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        traversal(root, result);
        return result;
    }
};
```
## 迭代遍历
前序遍历迭代  
关键是要注意node的更新迭代，而且这个例子非常清晰的显示了迭代法和栈之间的紧密联系
```
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> stk;
        stk.push(root);
        if (root == nullptr) return result;
        while (!stk.empty()) {
            TreeNode* node = stk.top();
            stk.pop();
            result.push_back(node->val);
            if (node->right) stk.push(node->right);
            if (node->left) stk.push(node->left);
        }
        return result;
    }
};
```
后序遍历迭代  
这个相比于前序遍历只用更改少量代码即可，前序代码是中左右，后序是左右中，将前序遍历迭代代码改成中右左，
最后把结果reverse过来就变成了左右中，即是后序遍历的结果（实测验证推导没问题）。

中序遍历迭代  
这个就不一样了，因为前序和后序都是先处理的中间节点，但是中序先处理的是左节点，所以无法通过上面代码修改得到结果。
中序遍历迭代法有些技巧，需要多练习或者记忆。
```
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> stk;
        TreeNode* cur = root;
        while (cur != nullptr || !stk.empty()) {
            if (cur != nullptr) {
                stk.push(cur);
                cur = cur->left;
            }
            else {
                cur = stk.top();
                stk.pop();
                result.push_back(cur->val);
                cur = cur->right;
            }
        }
        return result;
    }
};
```
## 统一迭代
统一迭代是为了用迭代法将三种遍历方式基于同一风格实现，解决访问节点和要处理节点的不一致问题。
解决这一问题可以将访问的节点放入栈中，把要处理的节点也放入栈中但是紧接着放一个空指针作为标记。

统一迭代的代码比较抽象，当前对我比较困难，暂时不使用该方法。
