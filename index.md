# 代码随想录第二天｜203移除链表元素 707设计链表 206反转链表
## 203 移除链表元素
该问题尤其需要注意的是，不要访问到空节点（nullptr）的next和val！

## 707 链表设计
该问题细节很多，链表末尾的寻找通过判断cur->next == nullptr;

## 206 反转链表
这道题其实很简单，但是细节在于对pre和cur的定义和赋值顺序，比如
```
pre = cur;
cur = temp;
```
而不是
```
cur = temp;
pre = cur;
```


<img width="357" alt="image" src="https://github.com/hbxysch/hbxysch.github.io/assets/50912459/8f3feb13-c53d-4ef1-b9e8-8b3765e2ea64">



