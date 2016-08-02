#<center>一天一道LeetCode系列</center>
##（一）题目
>Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

>For example, given the array [−2,1,−3,4,−1,2,1,−5,4],
>the contiguous subarray [4,−1,2,1] has the largest sum = 6.

##（二）解题
本题想到了两个思路：暴力求解法和分治法。前者就不多说了，本文主要讨论分治法。 
分治法的大致思路：对于A[low,high]这个数组，任何的连续子数组A[i,j]的位置必然是一下三种情况之一：

完全位于子数组A[low,mid]中，因此有low<=i<=j<=mid
完全位于子数组A[mid+1,high]中，因此mid<i<=j<=high
跨越了中点，因此low<=i<=mid<j<=high
对于前两种情况，只需要找出左右和右边的最大子数组即可。 
对于第三种情况，我们只需要找到A[i,mid]和A[mid+1,j]的最大子数组，然后相加即可。

```cpp

class Solution {

public:

    int maxSubArray(vector<int>& nums) {

        int len = nums.size();

        return findMaxSubArray(nums,0,len-1);

    }

    int findMaxSubArray(vector<int>& nums , int low , int high)

    {

        if(low==high) return nums[low];

        int mid = (low+high)/2;

        int left = findMaxSubArray(nums,low,mid);//子数组在左边的最大值

        int right = findMaxSubArray(nums,mid+1,high);//子数组在右边的最大值

        int cross = findMaxCrossSubArray(nums,low,high,mid);//子数组跨越中间点的时候的最大值

        if(left>=cross&&left>=right) return left;

        else if(right>=cross&&right>=left) return right;

        else return cross;//返回三个数的最大值

    }

    int findMaxCrossSubArray(vector<int>& nums , int low , int high , int mid)

    {

        int sum = 0;

        int left_sum = -2147483648;//int的最小数

        int right_sum = -2147483648;

        for(int i = mid ; i >= low ;i--)

        {

            sum+=nums[i];

            left_sum = left_sum<sum?sum:left_sum;//求左边的最大数

        }

        sum=0;

        for(int j = mid+1 ; j <= high;j++)

        {

            sum+=nums[j];

            right_sum = right_sum<sum?sum:right_sum;//求右边的最大数

        }

        return left_sum+right_sum;//返回和

    }

};

```