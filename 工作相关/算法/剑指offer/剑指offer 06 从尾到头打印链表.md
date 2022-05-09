## 题目

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

>**示例 1：**
>
>```
>输入：head = [1,3,2]
>输出：[2,3,1]
>```



### 实现一

使用栈作为辅助空间，此时时间复杂度为O(2n)，空间复杂度为O(n)。

```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        stack<int> stkNums;
        vector<int> nums;

        while(head)
        {
            stkNums.push(head->val);
            head = head->next;
        }
        while(!stkNums.empty())
        {
            nums.push_back(stkNums.top());
            stkNums.pop();
        }
        return nums;
    }
};
```



### 实现二

使用一个全局的vector存储数据，使用递归，递归终止条件为 p == nullptr。

```c++
class Solution {
public:
    vector<int> nums;
    void dfs(ListNode* p)
    {
        if(nullptr == p)
        {
            return;
        }
        dfs(p->next);
        nums.push_back(p->val);
    }
    vector<int> reversePrint(ListNode* head) {
        dfs(head);
        return nums;
    }
};
```

