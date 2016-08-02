#<center>一天一道LeetCode系列</center>
##(一)题目
> Given an array of integers, return indices of the two numbers such
> that they add up to a specific target.
> 
> You may assume that each input would have exactly one solution.
> 
> *Example: Given nums = [2, 7, 11, 15], target = 9,*
> 
> Because nums[0] + nums[1] = 2 + 7 = 9, return [0, 1]. UPDATE
> (2016/2/13): The return format had been changed to zero-based indices.
> Please read the above updated description carefully.

题目的意思是：输入一组数组和一个目标值，在数组中找出两个数，他们的和等于目标值，返回两个数的下标。

##(二)代码实现

初看题目我们可以很快得到以下的答案：

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> result;
        for(int i = 0 ; i < nums.size() ; ++i)
        {
            for(int j = i+1 ; j<nums.size() ; ++j)
            {
				if(nums[i]+nums[j] == target)
				{
					result.push_back(i);
					result.push_back(j);
					return result;
				}
			}
        }
    }
};
```
这样的解法的时间复杂度为O（N^2），提交代码后会报错Time Limit Exceeded。时间超限。

那么另寻他路，我们知道哈希表查找的时间复杂度是O（1），这里可以借助哈希表查找可以将时间复杂度降低到O（n）。

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int ,int> map;
        vector<int> result;
        for(int i = 0 ; i < nums.size() ; ++i)
        {
            if(map.find(target - nums[i])!=map.end())
            {
                if(map[target - nums[i]]!=i)
                {
                    result.push_back(map[target - nums[i]]);
                    result.push_back(i);
                    return result;
                }
            }
            map[nums[i]] = i;
        }
    }
};
```



