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
思路没问题，但是实现起来有点乱，没有掌握解耦的思想，需要把getSum函数拿出来单独实现，这样防止混乱

```
class Solution {
public:
    int getSum (int n) {
            int accum = 0;
            while(n/10 != 0) {
                accum += (n%10)*(n%10);
                n = n/10;
            }
            accum += n*n;
            return accum;
    }
    bool isHappy(int n) {
        unordered_set<int> record;
        while (1) {
            int sum = getSum(n);
            if (sum == 1) {
                return true;
            }
            else if ( record.find(sum) != record.end()) {
                return false;
            }
            else {
                record.insert(sum);
            }
            n = sum;
        }
    }
};
```

## 1.两数之和  
这个题主要考察map的用法，但是我还不是很熟，后面需要再重新回顾

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> map;
        for (int i = 0; i < nums.size(); i++) {
            unordered_map<int, int>::iterator ite = map.find(target - nums[i]);
            if (ite != map.end()) {
                return {ite->second, i};
            }
            map.insert(pair<int, int> (nums[i], i));
        }
        return {};
    }
};
```


