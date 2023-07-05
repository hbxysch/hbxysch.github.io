# 代码随想录第7天｜ 454.四数相加II 383. 赎金信 15. 三数之和 18. 四数之和

## 454 四数相加II
这个问题需要转换成2+2的问题就容易了，用map结构，key是a+b的和，value是出现次数

```
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int, int> sum_map;
        int sum = 0;
        for (int a:nums1) {
            for (int b:nums2) {
                sum_map[a+b]++;
            }
        }
        for (int c:nums3) {
            for (int d:nums4) {
                auto ite = sum_map.find(0-(c+d));
                if (ite != sum_map.end()) {
                    sum += ite->second;
                }
            }
        }
        return sum;
    }
};
```

## 383 赎金信
这部分思路和之前的异位词问题很接近，下面代码中第三个for循环可以塞进第二个里面

```
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        int record[26] = {0};
        for (int i = 0; i<magazine.size(); i++) {
            record[magazine[i] - 'a']++;
        }
        for (int i = 0; i<ransomNote.size(); i++) {
            record[ransomNote[i] - 'a']--;
        }
        // 下面的for循环可以并入上面
        for (int i = 0; i<26; i++) {
            if (record[i] < 0) {
                return false;
            }
        }
        return true;
    }
};
```




