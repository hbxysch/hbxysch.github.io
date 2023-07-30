# 代码随想录第25天｜216.组合总和III 17.电话号码的字母组合

## 216 组合总和
```
class Solution {
private:
    vector<vector<int>> result;
    vector<int> path;
    void backtracking (int k, int n, int sum, int startIndex) {
        if (path.size() == k) {
            if (sum == n) result.push_back(path);
            return;
        }
        for (int i = startIndex; i <= 9; i++) {
            sum += i;
            path.push_back(i);
            backtracking(k, n, sum, i + 1);
            sum -= i;
            path.pop_back();
        }
    }
public:
    vector<vector<int>> combinationSum3(int k, int n) {
        backtracking(k, n, 0, 1);
        return result;
    }
};
```
可以进行剪枝，就是判断sum大于目标值的时候就没必要继续搜索下去了。

## 17 电话号码的字母组合
这个题需要对电话号码和字母进行匹配。
```
class Solution {
private:
    const string letterMap[10] = {
        "",
        "",
        "abc",
        "def",
        "ghi",
        "jkl",
        "mno",
        "pqrs",
        "tuv",
        "wxyz"
    };
    vector<string> result;
    string path;
    void backtracking (const string& digits, int index) {
        if (index == digits.size()) {
            result.push_back(path);
            return;
        }
        int digit = digits[index] - '0';
        string letter = letterMap[digit];
        for (int i = 0; i < letter.size(); i++) {
            path.push_back(letter[i]);
            backtracking(digits, index+1);
            path.pop_back();
        }
    }
public:
    vector<string> letterCombinations(string digits) {
        if (digits.size() == 0) {
            return result;
        }
        backtracking(digits, 0);
        return result;
    }
};
```