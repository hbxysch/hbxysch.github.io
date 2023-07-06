# 代码随想录第一天｜704. 二分查找，27. 移除元素
## 704 二分查找
该问题关键在于定义二分法的区间开闭，这样才能保证所有的元素都被找到。
- 定义左闭右闭
- 定义左闭右开
<img width="415" alt="image" src="https://github.com/hbxysch/hbxysch.github.io/assets/50912459/0f4cb9e1-615c-4a2e-bf31-ed80f3fa9f06">

## 27 移除元素
该问题关键在于快慢指针，但是我写的不是很简洁。
需要注意：快指针每次循环都要++，慢指针在找到target的时候不++，基于这个就能设计更简单的代码，下面是答案代码和我的代码对比
<img width="460" alt="image" src="https://github.com/hbxysch/hbxysch.github.io/assets/50912459/10ac8f60-56f1-43de-9fda-9c4b4b5f2746">

    class Solution {
    public:
        int removeElement(vector<int>& nums, int val) {
            int slowIndex = 0;
            for (int fastIndex = 0; fastIndex < nums.size(); fastIndex++) {
                if (val != nums[fastIndex]) {
                    nums[slowIndex++] = nums[fastIndex];
                }
            }
            return slowIndex;
        }
    };
