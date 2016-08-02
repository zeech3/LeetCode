#<center>一天一道LeetCode系列</center>
##（一）题目

> Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
##（二）解题
这题是剑指offer上的老题了，剑指上面用的是递归，我写了个非递归的版本。
```cpp
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* head = NULL;
        if(l1==NULL && l2==NULL) return head;
        ListNode* p = NULL;
        ListNode* p1 = l1;
        ListNode* p2 = l2;
        while(p1 != NULL || p2!=NULL)
        {
            if(p1 != NULL && p2 != NULL)
            {
                if(p1->val < p2->val)
                {
                    if(head == NULL) //记录头节点head
                    {
                        head = p1;
                        p = head;
                    }
                    else {p->next = p1;p=p->next;}
                    p1=p1->next;
                    
                }
                else
                {
                    if(head == NULL) 
                    {
                        head = p2;
                        p = head;
                    }
                    else {p->next = p2;p=p->next;}
                    p2=p2->next;
                }
            }
            if(p1 == NULL && p2 != NULL)
            {
                if(head == NULL) 
                {
                    head = p2;
                    p = head;
                }
                else {p->next = p2;p=p->next;}
                p2=p2->next;
            }
            if(p1 != NULL && p2 == NULL)
            {
                if(head == NULL) 
                {
                    head = p1;
                    p = head;
                }
                else {p->next = p1;p=p->next;}
                p1=p1->next;
            }
        }
        return head;
    }
};
```
递归版本：

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL) return l2;
        if(l2 == NULL) return l1;
        ListNode* head;
        if(l1->val < l2->val)
        {
            head = l1;
            head->next = mergeTwoLists(l1->next , l2);
        }
        else
        {
            head = l2;
            head->next = mergeTwoLists(l1 , l2->next);
        }
        return head;
    }
};
```

