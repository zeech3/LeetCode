#<center>一天一道LeetCode系列</center>
##（一）题目
>Given an array of strings, group anagrams together.

>For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 
>Return:

>>[
>>  ["ate", "eat","tea"],
>>  ["nat","tan"],
>>  ["bat"]
>>]


>Note:

>>1.For the return value, each inner list's elements must follow the lexicographic order.

>>2.All inputs will be in lower-case.

##（二）解题
本题的解法是通过sort对单个string中的字符进行排序，排序后如果相同的就放在一个vector
注意：题目中的Note部分有提到返回的结果需要进行字典排序，一开始一直想不到办法，后来在讨论区看到有人直接用sort对里面的数进行排序就得出了字典排序，一下子恍然大悟！
```cpp
class Solution {

public:

    vector<vector<string>> groupAnagrams(vector<string>& strs) {

        vector<vector<string>> ret;

        map<string,int> nonrepstr;//用来存放排序后不重复的string

        int count = 0;//用来标识该string在ret中的位置

        for(int i = 0 ; i < strs.size() ; i++)

        {

            string tempstr = strs[i];

            sort(strs[i].begin(),strs[i].end(),less<char>());

            auto iter = nonrepstr.find(strs[i]);

            if(iter!=nonrepstr.end())//找到

            {

                (ret[iter->second]).push_back(tempstr);//如果找到了就放到ret里相应的vector中

            }

            else//没找到

            {

                nonrepstr.insert(pair<string, int>(strs[i],count++));//不重复的string放入map中

                vector<string> temp;

                temp.push_back(tempstr);

                ret.push_back(temp);//结果中也需要保存一份

            }

        }

        for(int j=0;j<count-1;j++)//输出结果要进行字典排序

        {

            sort(ret[j].begin(),ret[j].end());

        }

        return ret;

    }

};



```