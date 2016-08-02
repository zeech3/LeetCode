
#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.
If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

>You may not alter the values in the nodes, only nodes itself may be changed.

>Only constant memory is allowed.

>For example,
Given this linked list: 1->2->3->4->5

>For k = 2, you should return: 2->1->4->3->5

>For k = 3, you should return: 3->2->1->4->5

##（二）解题

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
    ListNode* reverseKGroup(ListNode* head, int k) {
        //主要思想：以K为间距，分别对间距内的链表进行反转
        //需要注意的问题：为了防止链表断裂需要记录每一段的首尾元素
        ListNode* pret = head;
        ListNode* phead = head;//当前待反转的head节点
        ListNode* ptail = NULL;//当前待反转的尾节点
        ListNode* pnexthead = NULL;.//记录下一段的head
        ListNode* plasttail = NULL;//记录前一段的尾节点
        if(head == NULL) return NULL;
        while(phead!=NULL)
        {
            int gap=k;
            ListNode* p = phead;
            while(gap != 1&& p!=NULL) {p = p->next;gap--;}//找到尾节点
            if(p!=NULL){
                ptail = p;
                ListNode* tmp;
                pnexthead = p->next;
                if(phead == head) pret = reverseK(phead,ptail,pnexthead);//0-k段的时候要记录整个链表的头节点
                else 
                {
                    tmp = reverseK(phead,ptail,pnexthead);
                    plasttail->next = tmp;
                }
                phead = pnexthead;//跳转到下一段
                plasttail = ptail;//记录当前段的尾节点
            }
            else 
            {
                if(plasttail!= NULL) plasttail->next = phead;//将[0-k]，[k+1-2k]......链接起来，防止链表断裂
                phead = NULL;//如果链接最后凑不够K个元素，则将phead置为NULL
            }
        }
        return pret;
    }
    ListNode* reverseK(ListNode* phead ,ListNode* &ptail/*注意此处用引用来获得尾节点*/,ListNode* pnexthead)
    {
        ListNode* prevHead = phead;
        ListNode* p = phead->next;
        ListNode* pre = phead;
        while(1)
        {
            if(p==pnexthead) {
               ptail = pre;//返回尾节点
               return prevHead; 
            }
            pre->next = p->next;
            p->next = prevHead;
            prevHead = p;
            p=pre->next;
        }
    }
};
```
