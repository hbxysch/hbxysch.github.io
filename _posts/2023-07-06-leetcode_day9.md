# 代码随想录第9天｜ 28. 实现 strStr() 459.重复的子字符串

## 28 实现strStr（）
该问题是KMP算法经典问题，需要深入完全理解KMP算法并且重新做

```
class Solution {
public:
    void getNext(int* next, string& s) {
        int j = 0;
        next[0] = 0;
        for (int i = 1; i < s.size(); i++) {
            while (j > 0 && s[i] != s[j]) {
                j = next[j - 1];
            }
            if (s[i] == s[j]) {
                j++;
            }
            next[i] = j;
        }
    }
    int strStr(string haystack, string needle) {
        int next[needle.size()];
        getNext(next, needle);
        int j = 0;
        for (int i = 0; i < haystack.size(); i++) {
            while (j > 0 && haystack[i] != needle[j]) {
                j = next[j-1];
            }
            if (haystack[i] == needle[j]) {
                j++;
            }
            if (j == needle.size()) {
                return (i-needle.size()+1);
            }
        }
        return -1;
    }
};
```

## 459 重复的子字符串
该问题还是使用KMP算法，思想是：最小相等前后缀不包含的字串就是最小重复字串

```
class Solution {
public:
    void getNext (int* next, string& s) {
        int j = 0;
        next[0] = 0;
        for (int i = 1; i < s.size(); i++) {
            while (j > 0 && s[i] != s[j]) {
                j = next[j-1];
            }
            if (s[i] == s[j]) {
                j++;
            }
            next[i] = j;
        }
    }
    bool repeatedSubstringPattern(string s) {
        int next[s.size()];
        getNext(next, s);
        int len = s.size();
        if (next[len-1] != 0 && len % (len - next[len-1]) == 0) {
            return true;
        }
        return false;
    }
};
```