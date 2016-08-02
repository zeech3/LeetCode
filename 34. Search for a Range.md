#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a sorted array of integers, find the starting and ending position of a given target value.

>Your algorithm's runtime complexity must be in the order of O(log n).

>If the target is not found in the array, return [-1, -1].

>For example,
>Given [5, 7, 7, 8, 8, 10] and target value 8,
>return [3, 4].

##（二）解题
```cpp
/*
首先二分法查找目标值
然后沿着目标值左右延伸，依次找到相同值得左右边界
*/
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int i = 0;
        int j = nums.size()-1;
        int idx = -1;
        vector<int> ret;
        while(i <= j)
        {
            int mid = (i+j)/2;
            if(nums[mid] == target)
            {
                idx = mid;
                break;
            }
            else if(nums[mid]>target)
            {
                j = mid-1;
            }
            else if(nums[mid]<target)
            {
                i = mid+1;
            }
        }
        if(idx!=-1){
            int k = idx;
            while(k>=0 && nums[k] == target) k--;
            int m = idx;
            while(m<nums.size()&&nums[m] == target) m++;
            ret.push_back(k+1);
            ret.push_back(m-1);
        }
        else{
            ret.push_back(-1);
            ret.push_back(-1);
        }
        return ret;
    }
};
```