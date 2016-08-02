

#<center>一天一道LeetCode系列</center>
----------


##（一）题目

>Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

##（二）解题

合并K个已拍好序的链表。剑指上有合并两个已排好序的链表的算法，那么K个数，我们可以采用归并排序的思想，不过合并函数可能需要修改一下，换成合并两个已排好序的链表的方法。代码如下：

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

    ListNode* mergeKLists(vector<ListNode*>& lists) {

        int len = lists.size();

        if(len == 0) return NULL;

        if(len == 1) return lists[0];

        ListNode* ret =  merge(lists,0,lists.size()-1);

        return ret;

    }

    ListNode* merge(vector<ListNode*>& lists , int i,int j){

        if(i==j) return lists[i];

        ListNode* ret = NULL;

        if(i<j){

            int mid = (i+j)/2;

            ListNode* lhs = merge(lists , i,mid);

            ListNode* rhs = merge(lists , mid+1,j);

            ret = mergeTwoLists(lhs,rhs);

        }

        return ret;

    }

    ListNode* mergeTwoLists(ListNode* list1 , ListNode* list2){

        if(list1 == NULL) return list2;

        if(list2 == NULL) return list1;

        

        ListNode* ret = NULL;

        

        if(list1->val < list2->val){

            ret = list1;

            ret->next = mergeTwoLists(list1->next ,  list2);

        }

        else{

            ret = list2;

            ret->next = mergeTwoLists(list1 ,  list2->next);

        }

        return ret;

    }

};

```