# 代码随想录第五天｜ 242.有效的字母异位词 349. 两个数组的交集 202. 快乐数 1. 两数之和  

## 242.有效的字母异位词 
该题用数组作为哈希表，要注意数组和string的用法

```
class Solution {
public:
    bool isAnagram(string s, string t) {
        int check[26] = {0};
        for (int i = 0; i<s.size(); i++) {
            check[s[i]-'a']++;
        }
        for (int i = 0; i<t.size(); i++) {
            check[t[i]-'a']--;
        }
        for (int i = 0; i<26; i++) {
            if (check[i] != 0 ) {
                return false;
            }
        }
        return true;
    }
};
```

## 349.两个数组的交集
可以用数组也可以用unordered_set，如果数组有大小限制就用数组，否则只能用unordered_set; 因为数组需要提前知道数组大小

```
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result;
        int hash[1000] = {0};
        for (int num:nums1) {
            hash[num] = 1;
        }
        for (int num:nums2) {
            if (hash[num] == 1) {
                result.insert(num);
            }
        }
        return vector<int> (result.begin(), result.end());
    }
};
```

## 202.快乐数


## 1.两数之和  

