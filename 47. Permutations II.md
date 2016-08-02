#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a collection of numbers that might contain duplicates, return all possible unique permutations.

>>For example,
>>[1,1,2] have the following unique permutations:
>>[1,1,2], [1,2,1], and [2,1,1].

##（二）解题

求全排列数。具体思路可以参考[【一天一道LeetCode】#46. Permutations](http://blog.csdn.net/terence1212/article/details/51362681)这篇博客。
不同之处：上一题没有重复的数字，这一题有重复的数字

```cpp


class Solution {

public:

    vector<vector<int>> permute(vector<int>& nums) {

        vector<vector<int>> ret;

        sort(nums.begin(),nums.end());

        do{

            ret.push_back(nums);

        }while(nextpermute(nums));

        return ret;

    }

    bool nextpermute(vector<int>& nums)

    {

        int i = nums.size() -2;

        while(i>=0 && nums[i] >= nums[i+1]) i--;//考虑到有相等的情况，这里需要找到第一个破坏非降序的数

        int j = nums.size()-1;

        while(j>=0 && nums[j] <= nums[i]) j--;//找到第一个大于i的数

        if(i>=0)

        {

            swap(nums[i],nums[j]);//交换i和j

            reverse(nums.begin()+i+1,nums.end());//将i以后的数反转

            return true;//如果还存在下一个全排列数就返回true

        }

        return false;//如果数组已经为倒序了就说明没有下一个了，返回false

    }

};

```

