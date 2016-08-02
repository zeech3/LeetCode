#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a list, rotate the list to the right by k places, where k is non-negative.

>For example:
>Given 1->2->3->4->5->NULL and k = 2,
>return 4->5->1->2->3->NULL.


##（二）解题
本题的思路：
1、找到倒数第K个节点
2、将k以后的节点移动到前面来，与头结点相连。
3、新的头结点就是倒数第k个节点。
需要注意一下几种特殊情况：
1、链表为空或者链表只有一个节点
2、k的值为0或者k的值大于链表的长度
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
    ListNode* rotateRight(ListNode* head, int k) {
        if(k==0||head == NULL || head->next==NULL) return head;
        ListNode* pkth =  head;//记录倒数第k个节点
        ListNode* pLast =  head;//记录最后一个节点
        ListNode* ptemp =NULL;//倒数第K+1个节点
        ListNode* p = head;
        int length = 0;
        while(p!=NULL)//求出链表的长度
        {
            p=p->next;
            ++length;
        }
        k %=length;//保证k在0~length之间
        if(k==0) return head;//k等于0直接返回head
        while(pLast != NULL && --k) pLast = pLast->next;//找到正数第K个节点
        while(pLast->next !=NULL){//找到倒数第K个节点
            ptemp = pkth;//这里用到两个指针，pLast和pkth同时移动，最后pkth就是倒数第K个节点
            pkth = pkth->next;
            pLast = pLast->next;
        }
        ptemp->next = NULL;
        pLast->next = head;//调整链表
        return pkth;
    }
};
```