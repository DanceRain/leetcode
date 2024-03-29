## 题目

>输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。
>
>例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。
>
>**示例：**
>
>```
>给定一个链表: 1->2->3->4->5, 和 k = 2.
>
>返回链表 4->5.
>```



今天的面试题，没想到双指针的方式，算法还是刷得太少了。left，right 首先同时指向头节点，然后 left 向后移动k次再同时移动 left 和 right 指针，这样当 right 指针为 nullptr 时 left 所指向的即为倒数第k个节点。

```c++
class Solution {
public:
    ListNode* getKthFromEnd(ListNode* head, int k) {
        if(head == nullptr)
        {
            return nullptr;
        }
        ListNode* left = head;
        ListNode* right = head;
        while(k--)
        {
            right = right->next;
        }
        while(right != nullptr)
        {
            right = right->next;
            left = left->next;
        }
        return left;
    }
};
```

