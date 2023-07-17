# 代码随想录第10天｜ 20. 有效的括号 1047. 删除字符串中的所有相邻重复项 150. 逆波兰表达式求值

## 20 有效的括号
判断有效括号，最好的工具就是栈，这也是代码底层数据结构使用的方式。判断可以分成三种情况：
1. 左边开括号多，右边闭括号少
2. 左边开括号少，右边闭括号多
3. 括号不匹配

```
class Solution {
public:
    bool isValid(string s) {
        stack<char> stk;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(') stk.push(')');
            else if (s[i] == '[') stk.push(']');
            else if (s[i] == '{') stk.push('}');
            else if (stk.empty() || stk.top() != s[i]) return false;
            else {
                stk.pop();
            }
        }
        return stk.empty();
    }
};
```
## 1047 删除字符串中的所有相邻重复项
利用栈的特性，但是要注意如何将栈中的内容转到字符串结果中去，并且要注意反转，因为栈先近后出。
```
class Solution {
public:
    string removeDuplicates(string s) {
        stack<char> stk;
        for (int i = 0; i < s.size(); i++) {
            if (!stk.empty() && stk.top() == s[i]) {
                stk.pop();
            }
            else {
                stk.push(s[i]);
            }
        }
        string result = "";
        while (!stk.empty()) {
            result += stk.top();
            stk.pop();
        }
        reverse(result.begin(), result.end());
        return result;
    }
};
```

## 150 逆波兰表达式求值
逆波兰表达式的优点：
1. 去掉括号后运算无歧义
2. 适合用栈操作运算：遇到数字则入栈，遇到运算符则取出栈顶两个元素并将计算结果压入栈中
```
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<long long> stk;
        for (int i = 0; i < tokens.size(); i++) {
            if (tokens[i] == "+" || tokens[i] == "-" || tokens[i] == "*" || tokens[i] == "/") {
                long long num2 = stk.top();
                stk.pop();
                long long num1 = stk.top();
                stk.pop();
                if (tokens[i] == "+") {
                    stk.push(num1+num2);
                }
                else if (tokens[i] == "-") {
                    stk.push(num1-num2);
                }
                else if (tokens[i] == "*") {
                    stk.push(num1*num2);
                }
                else if (tokens[i] == "/") {
                    stk.push(num1/num2);
                }
            }
            else {
                stk.push(stoll(tokens[i]));
            }
        }
        return stk.top();
    }
};
```