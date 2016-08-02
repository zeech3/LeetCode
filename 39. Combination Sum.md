#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the >candidate numbers sums to T.

>The same repeated number may be chosen from C unlimited number of times.

>Note:

>>All numbers (including target) will be positive integers.

>>Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).

>>The solution set must not contain duplicate combinations.



>For example, given candidate set 2,3,6,7 and target 7, 
>A solution set is: 
>[7] 
>[2, 2, 3]

##（二）解题

```cpp

/*

主要思路：

1.对目标vector排序，定义一个临时的vector容器tmp

2.采用动态规划和回溯法的方法，对于当前要添加到tmp的数num

(1)如果target<num，return；

(2)如果target>num,则继续在num和num以后的数中选择一个数相加；(此处需要考虑可以重复的组合)

(3)如果target==num，则代表找到

对于(2),(3)递归完成后需要将压入的数弹出，即采用回溯法的思想

*/


class Solution {

public:

    vector<vector<int>> ret;//结果

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {

        sort(candidates.begin(),candidates.end());//首先进行排序

        for(int idx = 0;idx<candidates.size();idx++)

        {

           if(idx-1>=0 && candidates[idx] == candidates[idx-1]) continue;//避免重复查找

           else{

               if(candidates[idx]<=target){//如果小于则调用动态规划函数

                  vector<int> tmp;

                  tmp.push_back(candidates[idx]);

                  combinationDfs(candidates,tmp,idx,target-candidates[idx]); 

               }

           }

        }

        return ret;

    }

    /*candidates为目标vector

    tmp为临时vector变量，存储找到的组合

    start是初始序号，代表在start及其以后的数字中查找

    target是当前需要在candidates中查找的数

    */

    void combinationDfs(vector<int>& candidates , vector<int>& tmp , int start,int target)

    {

        if(target == 0){//如果target等于0，代表第一个数就满足

            ret.push_back(tmp);

            return;

        }

        for(int idx = start;idx<candidates.size();idx++)

        {

            if(target > candidates[idx])

            {

                tmp.push_back(candidates[idx]);

                combinationDfs(candidates,tmp,idx,target-candidates[idx]);

                tmp.pop_back();//回溯法，要pop出最后压入的元素

            }

            else if(target == candidates[idx])//等于target代表以及找到

            {

                tmp.push_back(candidates[idx]);

                ret.push_back(tmp);

                tmp.pop_back();//回溯法，要pop出最后压入的元素

            }

            else if(target < candidates[idx])

            {

                return;

            }

        }

    }

};

```