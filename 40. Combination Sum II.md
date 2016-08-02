#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

>Each number in C may only be used once in the combination.

>Note:

>>All numbers (including target) will be positive integers

>>Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).

>>The solution set must not contain duplicate combinations.



>For example, given candidate set 10,1,2,7,6,1,5 and target 8, 
>A solution set is: 
>[1, 7] 
>[1, 2, 5] 
>[2, 6] 
>[1, 1, 6] 

##（二）解题
具体思路与[【一天一道LeetCode】39. Combination Sum](http://blog.csdn.net/terence1212/article/details/51308668)这篇博文一样，采用动态规划和回溯法进行求解。
```cpp
/*
和上一题的思路一样，区别是数字不能重复查找，但Vector中允许有重复的数字
具体改动请看代码注释
*/
class Solution {
public:
    vector<vector<int>> ret;
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(),candidates.end());
        for(int idx = 0;idx<candidates.size();idx++)
        {
           if(idx-1>=0 && candidates[idx] == candidates[idx-1]) continue;//避免重复查找
           else
           {
               if(candidates[idx]<=target)
               {//如果小于则调用动态规划函数
                  vector<int> tmp;
                  tmp.push_back(candidates[idx]);
                  combinationDfs(candidates,tmp,idx,target-candidates[idx]); 
               }
           }
        }
        return ret;
    }
    void combinationDfs(vector<int>& candidates ,vector<int>& tmp, int start ,int target)
    {
        if(target == 0){
            ret.push_back(tmp);
            return;
        }
        for(int i = start+1 ; i < candidates.size() ; i++)//从start+1开始查找，避免了数字重复查找
        {
            if(candidates[i] < target){
                tmp.push_back(candidates[i]);
                combinationDfs(candidates,tmp,i,target-candidates[i]);
                tmp.pop_back(); //回溯
            }
            else if(candidates[i] == target){
                tmp.push_back(candidates[i]);
                ret.push_back(tmp);
                tmp.pop_back();//回溯
            }
            else
            {
                return;
            }
            while(i+1< candidates.size()&&candidates[i]==candidates[i+1]) i++;//去除重复的查找
        }
    }
};
```