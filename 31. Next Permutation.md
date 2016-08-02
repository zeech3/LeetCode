#<center>一天一道LeetCode系列</center>
##（一）题目
>Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

>If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

>The replacement must be in-place, do not allocate extra memory.

>Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
>>1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1

##（二）解题

```

/*

本题用到STL中next_Permutation的思想：

（1）首先从右到左找到第一个破坏升序的值a，

（2）然后再从右至左找到第一个比a大的数b，

（3）交换a和b，

（4）再把交换后的a的位置之后的数反转。

如1,4,5,3,1

第一步找到4，第二步找到5，交换4,5得到15431，然后反转5以后的数，得到15134即为所求。

*/

class Solution {

public:

    void nextPermutation(vector<int>& nums) {

        int len = nums.size();

        if(len!=1){

            int i = len-2;

            while(i>=0 &&nums[i]>=nums[i+1]) i--;

            int j =len-1;

            while(j>i &&nums[j]<=nums[i]) j--;

            if(i>=0) swap(nums[i],nums[j]);

            reverse(nums.begin()+i+1,nums.end());

        }

    }

};

```