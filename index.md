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

## 15 三数之和
a+b+c = 0;
关于去重，排序之后，如果a重复就不用考虑，因为(b+c)==-a的所有b和c都已经之前找出来了。

找到答案时，为了防止重复，left和right双指针同时收缩

这个问题b和c的去重，要和后一个元素相比，和前一个元素相比没有意义，因为是往内搜索

```
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        sort(nums.begin(), nums.end());
        for (int i = 0; i<nums.size(); i++) {
            if (i>0 && (nums[i] == nums[i-1])) {
                continue;
            }
            int left = i+1;
            int right = nums.size()-1;
            while (left<right) {
                if (nums[i] + nums[left] + nums[right] == 0) {
                    result.push_back(vector<int> {nums[i], nums[left], nums[right]});
                    while (left<right && (nums[left] == nums[left+1])) left++;
                    while (left<right && (nums[right] == nums[right-1])) right--;
                    right--;
                    left++;
                }
                else if (nums[i] + nums[left] + nums[right] < 0) left++;
                    
                else if (nums[i] + nums[left] + nums[right] > 0) right--;
            }
        }
        return result;
    }
};
```

## 18 四数之和
四数之和重要的一点是：在剪枝操作的时候，两个数相加可能越来越小（因为有负数），所以不能直接做剪枝操作
其余思路和三数之和一样，就是加了一层for循环

```
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> result;
        sort(nums.begin(), nums.end());
        for (int i = 0; i<nums.size(); i++) {
            if (nums[i] > target && nums[i] >= 0) {
                break; 
            }
            if (i>0 && (nums[i] == nums[i-1])) continue;
            for (int j = i+1; j<nums.size(); j++) {
                if (nums[i] + nums[j] > target && nums[i] + nums[j] >= 0) {
                    break;
                }
                if (j>i+1 && (nums[j] == nums[j-1])) continue;
                int left = j+1;
                int right = nums.size() - 1;
                while (left<right) {
                    if ((long) nums[i] + nums[j] + nums[left] + nums[right] > target) right--;
                    else if ((long) nums[i] + nums[j] + nums[left] + nums[right] < target) left++; 
                    else {
                        result.push_back(vector<int> {nums[i], nums[j], nums[left], nums[right]});
                        while (left<right && nums[left] == nums[left+1]) left++;
                        while (left<right && nums[right] == nums[right-1]) right--;
                        left++;
                        right--;
                    }
                }
            }
        }
        return result;
    }
};
```



