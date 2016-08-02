#<center>一天一道LeetCode系列</center>
##（一）题目

> Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
> 
>     For example, given array S = {-1 0 1 2 -1 -4},
>     A solution set is:
>     (-1, 0, 1)
>     (-1, -1, 2)
##（二）解题
这道题的关键在于：结果集合中不允许有重复。
想到的方法有两个：1、在查找过程中去重 2、在结果中去重
经过试验，结果中去重会直接超时。
1、过程中去重版本
```
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> vecresult;
        std::sort(nums.begin(),nums.end());
        int len = nums.size();
        if(len <3) return vecresult;
        for(int i = 0 ; i < nums.size() ;)
        {
            if(nums[i]>0) return vecresult;
            for(int j = i+1;j<nums.size()-1;)
            {
                int temp = 0-nums[i]-nums[j];
                vector<int>::iterator iter = find(nums.begin()+j+1,nums.end(),temp);
                if(iter != nums.end())
                {
                    vector<int> tempres;
                    tempres.push_back(nums[i]);
                    tempres.push_back(nums[j]);
                    tempres.push_back(*iter);
                    vecresult.push_back(tempres);
                }
                j++;
                while(j<nums.size()&&nums[j]==nums[j-1]) ++j;//去重
            }
            i++;
            while(i<nums.size()&&nums[i]==nums[i-1]) ++i;//去重
        }
        return vecresult;
    }
};
```
2、结果中去重版本（超时）

```
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> vecresult;
        std::sort(nums.begin(),nums.end());
        int len = nums.size();
        if(len <3) return vecresult;
        for(int i = 0 ; i < nums.size() ; i++)
        {
            if(nums[i]>0) return vecresult;
            for(int j = i+1;j<nums.size()-1;j++)
            {
                int temp = 0-nums[i]-nums[j];
                vector<int>::iterator iter = find(nums.begin()+j+1,nums.end(),temp);
                if(iter != nums.end())
                {
                    vector<int> tempres;
                    tempres.push_back(nums[i]);
                    tempres.push_back(nums[j]);
                    tempres.push_back(*iter);
                    if(vecresult.size()==0)
                    {
                        vecresult.push_back(tempres);
                    }
                    else{
                        vector<vector<int>>::iterator it1 = find(vecresult.begin(),vecresult.end(),tempres);
                        if(it1 == vecresult.end())//结果中去重
                        {
                            vecresult.push_back(tempres);
                        }
                    }
                }
            }
        }
        return vecresult;
    }
};
```