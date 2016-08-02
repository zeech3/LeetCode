#<center>一天一道LeetCode系列</center>
##（一）题目：

> Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
> 	> For example, given array S = {-1 2 1 -4}, and target = 1. The sum that
> 	> is closest to the target is 2. (-1 + 2 + 1 = 2).
##（二）解题
直接用三重循环，然后考虑到重复的数字，则需要先排序，以便于后续去重。
其次，当等于target时，则直接返回
```
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int min = 2147438647;
        int key =0;
        std::sort(nums.begin() , nums.end());
        for(int i = 0  ; i < nums.size()-2 ; )
        {
            for(int j = i+1 ; j < nums.size()-1 ;)
            {
                for(int k = j+1 ; k < nums.size() ; )
                {
                    int gap = nums[i]+nums[j]+nums[k];
                    int temp = gap-target>0?gap-target:target-gap;
                    if(temp<min){ 
                        min = temp;
                        key = gap;
                        if(min ==0)  //如果找到等于0的则返回
                        {
                            return key;
                        }
                    }
                    k++;
                    while(k<nums.size() && nums[k] == nums[k-1]) ++k;
                }
                j++;
                while(j<nums.size()-1 && nums[j] == nums[j-1]) ++j;
            }
            i++;
            while(i<nums.size()-2 && nums[i] == nums[i-1]) ++i;
        }
        return key;
    }
};
```
在网上看到另外一种快速的解法。O（n^2）
```
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        std::sort(nums.begin() , nums.end());
        bool isfirst = true;
        int ret;
        for(int i = 0  ; i < nums.size() ; i++)
        {
            int j = i+1;
            int k = nums.size()-1;
            while(j<k){
                int sum = nums[i]+nums[j]+nums[k];
                if(isfirst)
                {
                    ret = sum;
                    isfirst = false;
                }
                else
                {
                    if(abs(sum - target) < abs(ret - target))
                    {
                        ret = sum;
                    }
                }
                if(ret == target)
                    return ret;
                if(sum>target)
                    k--;
                else
                    j++;
            }
        }
        return ret;
    }
};
```