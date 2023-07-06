# 代码随想录第二天｜977 有序数组的平方 209 长度最小的子数组 59 螺旋矩阵
## 977 
最开始使用冒泡排序，时间复杂度比较高

<img width="465" alt="image" src="https://github.com/hbxysch/hbxysch.github.io/assets/50912459/d0248910-d82a-43d1-b577-a32a484f3d08">

要注意数组本身是有序的，只不过有正负，所以有个信息就是平方之后最大数一定在两侧，最小数在中间
学习该问题思路之后再写：这块儿index一定要清晰，因为是从两边往里搜索，所以要从右往左补充递增数组。

<img width="462" alt="image" src="https://github.com/hbxysch/hbxysch.github.io/assets/50912459/6de50ddd-eee6-48c7-ba43-72db3d835e52">

## 209
该题的关键是滑动窗口法，其实基本思路就是
1. 用滑动窗口（双指针）找到大于等于target的subarray
2. 然后缩小窗口进行查询是否有更小的数组长度
3. 如果找得到符合条件的subarray，则输出对应数组长度；找不到的话返回0

<img width="560" alt="image" src="https://github.com/hbxysch/hbxysch.github.io/assets/50912459/9bf3034a-cd8b-4c06-98bf-24c7879561a2">


## 59
该题的关键是掌握前闭后开的区间定义，这个搞清楚再注意二维vector数组的定义即可解题

<img width="403" alt="image" src="https://github.com/hbxysch/hbxysch.github.io/assets/50912459/33dc26b3-0ad8-437d-aabd-64cb2d8a0b19">


