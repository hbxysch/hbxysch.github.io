# 代码随想录第四天｜24. 两两交换链表中的节点｜ 19.删除链表的倒数第N个节点｜ 面试题 02.07. 链表相交｜ 142.环形链表II 

## 24 两两交换链表中的节点

<img width="542" alt="image" src="https://github.com/hbxysch/hbxysch.github.io/assets/50912459/0fa03a6b-5059-4944-98b0-5d4fbe7e3712">

这道题加上dummyHead其实就很简单了，直接使用链表的指针改变指向顺序即可，要注意保存中间的指针信息。

## 19 删除链表中倒数第N个节点
这道题关键在于fast和slow指针之间的距离确定，如果删除倒数第n个元素，需要将fast指针往前移动n+1步，然后同时和slow指针向右移动直到指向nullptr

```
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummyHead = new ListNode(0);
        dummyHead->next = head;
        ListNode* slow = dummyHead;
        ListNode* fast = dummyHead;
        for(int i=0; i<n+1; i++){
            fast = fast->next;
        }
        while(fast != nullptr){
            slow = slow->next;
            fast = fast->next;
        }
        ListNode* tmp = slow->next;
        slow->next = slow->next->next;
        delete tmp;
        return dummyHead->next;
    }
};
```

## 面试题 链表相交
该问题不难，由于是两个链表相交，所以需要将尾端对齐然后从较短链表的头部进行比较。

  class Solution {
  public:
      ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
          ListNode* curA = headA;
          ListNode* curB = headB;
          int countA = 0;
          int countB = 0;
          while (curA != nullptr) {
              curA = curA->next;
              countA++;
          }
          while (curB != nullptr) {
              curB = curB->next;
              countB++;
          }
          if (countA > countB) {
              curB = headB;
              curA = headA;
              int diff = countA - countB;
              while (diff--) {
                  curA = curA->next;
              }
          }
          else {
              curB = headB;
              curA = headA;
              int diff = countB - countA;
              while (diff--) {
                  curB = curB->next;
              }
          }
          while (curA != nullptr) {
              if (curA == curB) {
                  return curA;
              }
              curA = curA->next;
              curB = curB->next;
          } 
          return nullptr;
      }
  };

## 环形链表
寻找链表环的起始节点，该题第一次遇到，需要注意数学关系，分析步骤如下：
1. 定义快慢指针，找到两个节点相遇的节点
2. 在相遇的点通过数学关系定义index找到节点

还有个关键内容就是while中的判断：如果{}里面出现fast->next->next，while中需要判断fast和fast->next是否为空

```
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast != nullptr && fast->next != nullptr){
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                ListNode* index1 = head;
                ListNode* index2 = slow;
                while (index1 != index2) {
                    index1 = index1->next;
                    index2 = index2->next;
                }
                return index1;
            }
        }
        return nullptr;
    }
};
```








