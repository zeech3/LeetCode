#<center>一天一道LeetCode</center>
##（一）题目

> Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.
> 
> Note: Elements in a quadruplet (a,b,c,d) must be in non-descending
> order. (ie, a ≤ b ≤ c ≤ d) The solution set must not contain duplicate
> quadruplets.
> 
>     For example, given array S = {1 0 -1 0 -2 2}, and target = 0.
>     A solution set is:
>     (-1,  0, 0, 1)
>     (-2, -1, 1, 2)
>     (-2,  0, 0, 2)
##（二）解题
勉强不超时的代码。(注：和3sum比较类似)
```
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> result;
        if(nums.size()<4) return result;
        sort(nums.begin(),nums.end());
        for(int i = 0 ; i < nums.size()-3 ; )
        {
            for(int j=i+1 ; j < nums.size()-2 ; )
            {
                int start = j+1;
                int end = nums.size()-1;
                while(start<end)
                {
                    int sum = nums[i]+nums[j]+nums[start]+nums[end];
                    if(sum==target)
                    {
                        vector<int> vec;
                        vec.push_back(nums[i]);
                        vec.push_back(nums[j]);
                        vec.push_back(nums[start]);
                        vec.push_back(nums[end]);
                        result.push_back(vec);
                        start++;
                        while(start<end && nums[start] == nums[start-1]) start++;
                        end--;
                        while(start<end && nums[end] == nums[end+1]) end--;
                    }
                    else if(sum>target)
                    { 
                        end--;
                        while(start<end && nums[end] == nums[end+1]) end--;
                    }
                    else {
                        start++;
                        while(start<end && nums[start] == nums[start-1]) start++;;
                    }
                }
                j++;
                while(j<nums.size()-2 && nums[j] == nums[j-1]) j++;
            }
            i++;
            while(i<nums.size()-3 && nums[i] == nums[i-1]) i++;               
        }
        return result;
    }
};
```