#<center>一天一道LeetCode系列</center>
##（一）题目
>Given an array of non-negative integers, you are initially positioned at the first index of the array.

>Each element in the array represents your maximum jump length at that position.

>Your goal is to reach the last index in the minimum number of jumps.

>For example:
>Given array A = [2,3,1,1,4]

>The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

>Note:
>You can assume that you can always reach the last index.

##（二）解题
1、首先想到的做法就是对于序号i，判断i+nums[i]能不能到达终点，如果能直接return，如果不能对小于nums[i]的数依次进行递归，得到最小的min值。这种做法直接超时了，TLE！
```cpp
class Solution {
public:
    int min;
    int jump(vector<int>& nums) {
        min = nums.size();
        jumpdfs(nums,0,0);
        return min;
    }
    void jumpdfs(vector<int>& nums , int idx , int count)
    {
        int len = nums.size();
        if(idx >= len -1) {
            min = count;
            return;
        }
        if(idx<len && idx + nums[idx] >= len-1){
            min = min>(count+1)?(count+1):min;
            return;
        }
        else
        {
            for(int i = 1 ; idx<len && i<= nums[idx] ; i++)
            {
                jumpdfs(nums,idx+i,count+1);
            }
        }
    }
    
};
```
2、然后看到提示中有提到贪心算法，于是联想到昨天做的通配符那题，可以记录上一跳能达到的最远位置，和当前跳所能到达的最远位置，每次循环就更新这两个值，直到上一跳能达到终点就退出。
```cpp
/*
思路：贪心算法是假定每一次都作出当前的最优解，所以对于本题，每次记录当前的最远位置，和上一跳的最远位置。
*/
class Solution {
public:
    int jump(vector<int>& nums) {
        int ret = 0 ;
        int last = 0;
        int cur = 0;
        for(int i = 0 ; i < nums.size() ; i++)
        {
            if(last>=nums.size()-1) break;
            if(i>last)//如果当前位置已经跳出了上一跳的最远位置
            {
                last = cur;//更新上一跳的最远位置等于当前跳的最远位置
                ++ret;//跳的次数加1
            }
            cur = max(cur , i+nums[i]);//更新当前跳的最远位置
        }
        return ret;
    }
};
```