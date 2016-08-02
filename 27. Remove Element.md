#<center>一天一道LeetCode系列</center>
##（一）题目
>Given an array and a value, remove all instances of that value in place and return the new length.

>Do not allocate extra space for another array, you must do this in place with constant memory.

>The order of elements can be changed. It doesn't matter what you leave beyond the new length.

>Example:
>Given input array nums = [3,2,2,3], val = 3

>Your function should return length = 2, with the first two elements of nums being 2.

##（二）解题

解题思路见注释

```cpp

/*

在一个vector中删除指定的元素，用到erase()函数，注意迭代器会失效

erase()会返回被删除元素的下一个元素的迭代器

*/

class Solution {

public:

    int removeElement(vector<int>& nums, int val) {

        for(auto iter = nums.begin();iter!=nums.end();){

            if(*iter == val){

                iter = nums.erase(iter);//iter指向被删除元素的下一个元素

            }

            else

                ++iter;

        }

        return nums.size();

    }

};

```