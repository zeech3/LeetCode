#<center>一天一道leetcode系列</center>
###（一）题目：
> You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
> 
> Input: (2 -> 4 -> 3) + (5 -> 6 -> 4) Output: 7 -> 0 -> 8

题目意思： 输入两个倒序的多位数，输出它们的和。


###（二）代码实现：
一看到这个题，为了图简便，直接转换成int相加，然后转成链表，结果是**Memory Limit Exceeded** 提示超出内存限制
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int a=0,b=0;
        while(l1) {
            a=a*10+l1->val;
            l1=l1->next;
        }
        while(l2) {
            b=b*10+l2->val;
            l2=l2->next;
        }
        int temp = a+b;
        int temp_m = temp%10;
        temp = temp/10;
        ListNode* head = new ListNode(temp_m);
        ListNode* p = head;
        while(temp/10)
        {
            temp_m = temp%10;
            ListNode* next = new ListNode(temp_m);
            p->next = next;
            p=p->next;
        }
        return head;
    }
};
```

无奈，只能老老实实得按加法原则来求和了。

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* p = l1->next;
        ListNode* q = l2->next;
        bool jwflag = false;//进位标志位
        int temp = l1->val + l2->val;
        if(temp>=10) jwflag = true;
        ListNode* head = new ListNode(temp%10);
        ListNode* m = head;
        while(p && q)
        {
            if(jwflag) {temp = p->val+q->val +1;jwflag = false;}
            else temp = p->val+q->val;
            ListNode* ltemp = new ListNode(temp%10);
            if(temp>=10) jwflag = true;//处理进位
            m->next = ltemp;
            m = ltemp;
            p=p->next;
            q=q->next;
        }
        while(!p&&q) //p为空，q非空
        {
            if(jwflag) {temp = q->val +1;jwflag = false;}
            else temp = q->val;
            ListNode* ltemp = new ListNode(temp%10);
            if(temp>=10) jwflag = true;
            m->next = ltemp;
            m = ltemp;
            q = q->next;
        }
        while(p&&!q) //q为空，p非空
        {
            if(jwflag) {temp = p->val +1;jwflag = false;}
            else temp = p->val;
            ListNode* ltemp = new ListNode(temp%10);
            if(temp>=10) jwflag = true;
            m->next = ltemp;
            m = ltemp;
            p = p->next;
        }
        //处理最后一位的进位
        if(jwflag)
        {
            ListNode* ltemp = new ListNode(1);
            jwflag = false;
            m->next = ltemp;
            m = m->next;
        }
        return head;
        
    }
};
```
结果：Accepted。