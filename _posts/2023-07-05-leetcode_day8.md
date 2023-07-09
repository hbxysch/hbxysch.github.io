# 代码随想录第8天｜ 344.反转字符串 541. 反转字符串II 剑指Offer 05.替换空格 151.翻转字符串里的单词 剑指Offer58-II.左旋转字符串

## 344 反转字符串
该题非常简单，直接双指针,然后交换即可

```
class Solution {
public:
    void reverseString(vector<char>& s) {
        for (int i = 0, j = s.size()-1; i<=j; i++, j--) {
            swap(s[i], s[j]);
        }
    }
};
```

## 541 反转字符串II
该问题也比较简单，间隔2k进行reverse操作，可以自定义reverse函数也可以用库函数

下面代码中需要注意if判断中也可以直接用continue，然后取消else

```
class Solution {
public:
    void doReverse (string& s, int start, int end) {
        for (int i = start, j = end; i<j; i++, j--) {
            swap(s[i], s[j]);
        }
    }
    string reverseStr(string s, int k) {
        for (int i = 0; i < s.size(); i += (2*k)) {
            if ((i+k) <= s.size()) {
                doReverse(s, i, i+k-1);
            }
            else {
                doReverse(s, i, s.size()-1);
            }
        }
    return s;  
    }
};
```

## 剑指offer 05 替换空格
数组填充类问题，很多都可以预先扩容到添加元素之后的大小，然后从后往前操作，该题代码实现起来还是比较容易

```
class Solution {
public:
    string replaceSpace(string s) {
        int count = 0;
        int j = s.size() - 1;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == ' ') count++;
        }
        s.resize(s.size() + 2*count);
        int i = s.size() - 1;
        for (; j>=0; j--) {
            if (s[j] == ' ') {
                s[i--] = '0';
                s[i--] = '2';
                s[i] = '%';
            }
            else {
                s[i] = s[j];
            }
            i--;
        }
        return s;
    }
};
```

## 151 翻转字符串里的单词
分为三步：
1. 消除所有多余的空格
2. 将整个字符串反转
3. 再将每个单词反转回来
其中第一步需要再回顾，重新做

```
class Solution {
public:
    void doReverse(string& s, int start, int end) {
        while(start<end) {
            swap(s[start], s[end]);
            start++;
            end--;
        }
    }
    void removeExtraSpace (string& s) {
        int slow = 0;
        for (int fast = 0; fast < s.size(); fast++) {
            if (s[fast] != ' ') {
                if (slow != 0) s[slow++] = ' ';
                while (fast<s.size() && s[fast] != ' ') {
                    s[slow++] = s[fast++];
                }
            }
        }
        s.resize(slow);
    }
    string reverseWords(string s) {
        removeExtraSpace(s);
        doReverse(s, 0, s.size()-1);
        int start = 0, end = 0;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] != ' ') continue;
            end = i-1;
            doReverse(s, start, end);
            start = i+1;
        }
        doReverse(s, start, s.size()-1);
        return s;
    }
};
```


## 剑指Offer58-II 左旋转字符串
