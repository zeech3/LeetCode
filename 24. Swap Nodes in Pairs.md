#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a linked list, swap every two adjacent nodes and return its head.
For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

##（二）解题
给定一个链表，交换相邻两个节点，这道题要特别注意越界问题。

评级easy的题！就不多废话了。

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
    ListNode* swapPairs(ListNode* head) {
        if(head == NULL) return NULL;
        ListNode* p = head;
        ListNode* pnext = head->next;
        while(p!=NULL&&pnext!=NULL)
        {
            int tmp = pnext->val;
            pnext->val = p->val;
            p->val = tmp;
            if(pnext->next !=NULL) p = pnext->next; //考虑越界问题,如[1,2,3,4]
            else p=NULL;
            if(p!= NULL && p->next != NULL) pnext = p->next;//考虑越界问题，如[1,2,3,4,5]
            else pnext=NULL;
        }
        return head;
    }
};
```