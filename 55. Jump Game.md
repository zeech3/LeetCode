#<center>一天一道LeetCode系列</center>
##（一）题目

>Given an array of non-negative integers, you are initially positioned at the first index of the array.
Each element in the array represents your maximum jump length at that position.
Determine if you are able to reach the last index.
For example:
A = [2,3,1,1,4], return true.
A = [3,2,1,0,4], return false.

##（二）解题

思路可以参考这篇博文：[【一天一道LeetCode】#45. Jump Game II](http://blog.csdn.net/terence1212/article/details/51353209)

考虑在O(n)复杂度的情况下解决此题。用两个参数来lastmax和curmax来存储i前面能跳到的最远距离和当前能跳到的最远距离，如果此刻i还在lastmax之内，就要更新lastmax的值为max(lastmax,curmax)

```cpp

/*

代码很简单，主要注意两个点：

1、i小于lastmax才能改变lastmax的值

2、是否能跳到重点取决于lastmax的值

*/

class Solution {

public:

    bool canJump(vector<int>& nums) {

        int lastmax = 0;

        int curmax = 0;

        for(int i = 0 ; i < nums.size() ; i++)

        {

            curmax = i+nums[i];

            if(i<=lastmax)

            {

                lastmax = max(lastmax,curmax);

            }

        }

        if(lastmax >=nums.size()-1) return true;

        else return false;

    }

};

```