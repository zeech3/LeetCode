#<center>一天一道LeetCode系列</center>
##（一）题目

> Given a linked list, remove the nth node from the end of list and return its head.
> 
>> For example,    
> Given linked list: 1->2->3->4->5, and n = 2.    After
> removing the second node from the end, the linked list becomes 1->2->3->5.
##（二）解题
剑指上面的经典题目了。两个指针，一个指向head，一个指向正数第K-1个，同时移动，知道第K-1的指针指向NULL。则指向head的数就是倒数第K个。
删除节点的时候要区分头节点和其他节点。

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if(n == 0) return head;
        ListNode* ptemp = head;
        for(int i = 0 ; i < n ;i++)
        {
            ptemp = ptemp->next;
        }
        ListNode* pNth = head;
        ListNode* pre = head;
        while(ptemp!= NULL)
        {
            pre = pNth;
            ptemp = ptemp->next;
            pNth = pNth->next;
        }
        if(pNth == head)//如果是头节点
        {
            head = head->next;
        }
        else pre->next = pNth->next;//非头节点
        free(pNth);
        return head;
    }
};
```