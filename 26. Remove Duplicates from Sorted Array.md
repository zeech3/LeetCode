#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

>Do not allocate extra space for another array, you must do this in place with constant memory.

>For example,
>Given input array nums = [1,1,2],

>Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

##（二）解题

```cpp

/*

解题:排好序的数据，删除里面重复的数据

需要注意以下两点：

1.erase()调用之后迭代器失效，需要将iter = nums.erase(iter);

2.考虑nums为空或者只有1个的情况，可以直接返回

*/

class Solution {

public:

    int removeDuplicates(vector<int>& nums) {

        if(nums.size()<=1) return nums.size();

        auto iter = nums.begin() +1;

        for(;iter!=nums.end();)

        {

            if(*iter == *(iter-1))

            {

                iter = nums.erase(iter);//关键！erase()返回的是删除的数据的下一个迭代器

            }

            else

                ++iter;//没有删除元素的时候+1

        }

        return nums.size();

    }

};

```