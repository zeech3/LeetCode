#<center>一天一道LeetCode系列</center>
##（一）题目
>Given an unsorted integer array, find the first missing positive integer.

>For example,
>Given [1,2,0] return 3,
>and [3,4,-1,1] return 2.

>Your algorithm should run in O(n) time and uses constant space.

##（二）解题

```cpp
/*
首先对初始vector进行排序，然后设定一个target=1
从第一个大于0的数开始，如果等于target的数后就+1，直到下一个数不能于target为止
如果不能于就返回target
如果数组中找完了都没有返回，则返回target+1；
当然这里要考虑一种特殊情况：数组中有重复的数需要排除
*/
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int target = 1;
        for(int i = 0 ; i < nums.size() ; i++)
        {
            if(nums[i]>0)
            {
                if(nums[i] == target)
                {
                    target++;//注意这里已经+1了，最后返回直接返回target
                }
                else if(i>0 &&nums[i]!=nums[i-1])//排除重复数字
                {
                    return target;
                }
            }
        }
        return target;//如果找不到空缺的就返回target+1
    }
};
```