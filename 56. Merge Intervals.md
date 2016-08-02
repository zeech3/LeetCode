#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a collection of intervals, merge all overlapping intervals.

>For example,
>Given [1,3],[2,6],[8,10],[15,18],
>return [1,6],[8,10],[15,18].

##（二）解题

```cpp

/*

本题的解题步骤：

1、对vector里面的每个Interval结构体按照start的值升序排列

2、遍历整个intervals，如果有重复区域就合并，如果没有就存到ret里面

*/

/**

 * Definition for an interval.

 * struct Interval {

 *     int start;

 *     int end;

 *     Interval() : start(0), end(0) {}

 *     Interval(int s, int e) : start(s), end(e) {}

 * };

 */

class Solution {

public:

    vector<Interval> merge(vector<Interval>& intervals) {

        vector<Interval> ret;

        if(intervals.empty()) return ret;

        sort(intervals.begin(),intervals.end(),comparein);///按照start的值升序排列

        Interval tmp = intervals[0];//初始化

        for(int i = 1 ; i < intervals.size() ; i++)

        {

            if(intervals[i].start<=tmp.end) tmp.end = max(tmp.end,intervals[i].end);//更新end

            else{

                ret.push_back(tmp);//没有重复区域就压入ret

                tmp = intervals[i];//更新tmp的值，继续遍历

            }

        }

        ret.push_back(tmp);

        return ret;

    }

    static bool comparein(const Interval& i1 , const Interval& i2)//比较函数

    {

        return i1.start<i2.start;

    }

};

```