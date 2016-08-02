#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would >be if it were inserted in order.

>You may assume no duplicates in the array.

>Here are few examples.
>[1,3,5,6], 5 → 2
>[1,3,5,6], 2 → 1
>[1,3,5,6], 7 → 4
>[1,3,5,6], 0 → 0

##（二）解题

```cpp

/*

本题的思路是：如果目标数大于vector中的最大数，就返回vector的长度，即插在最后面

如果目标是小于vector中的最小数，就返回0，即插在最前面

如果在vector范围内，就用二分法查找，如果有等于target就返回其序号，如果没有即在i=j时退出，返回i表示target的插入位置

*/


class Solution {

public:

    int searchInsert(vector<int>& nums, int target) {

        int len = nums.size();

        if(target > nums[len-1]) return len;

        if(target < nums[0]) return 0;

        int i = 0;

        int j = len-1;

        while(i<=j)

        {

            int mid = (i+j)/2;

            if(nums[mid] == target) return mid;

            else if(nums[mid]>target) j=mid-1;

            else i = mid+1;

        }

        return i;

    }

};

```