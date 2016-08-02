#<center>一天一道LeetCode系列</center>
##（一）题目
>Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

>You may assume that the intervals were initially sorted according to their start times.

> **Example 1**:
>Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].

> **Example 2**:
>Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].

>This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

##（二）解题

相关题目：[【一天一道LeetCode】#56. Merge Intervals](http://blog.csdn.net/terence1212/article/details/51476535)

```cpp

/*

主要解题思路：

1、当intervals[i].end<newInterval.start的时候，不需要合并，直接i++

2、当找到第一个满足intervals[i].end>newInterval.start的时候，确定合并后的interval的start值

3、当找到最后一个满足intervals[i].start>newInterval.end的时候，确定合并后的interval的end值

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

    vector<Interval> insert(vector<Interval>& intervals, Interval newInterval) {

        vector<Interval> ret;

        if(intervals.size()==0){//特殊情况

            ret.push_back(newInterval);

            return ret;

        }

        int i = 0;

        Interval tmp;

        while(i<intervals.size()&&intervals[i].end<newInterval.start) {//将不需要合并的Interval直接压入ret

            ret.push_back(intervals[i]);

            i++;

        }

    ﻿    ﻿//找到了第一个满足intervals[i].end>newInterval.start的i值

    ﻿    ﻿//这里需要注意当newInterval比vector里面的值都大的情况

        tmp.start = min(i==intervals.size()?newInterval.start:intervals[i].start,newInterval.start);

        tmp.end = newInterval.end;

        while(i<intervals.size()&&intervals[i].start<=newInterval.end)

        {

            tmp.end = max(intervals[i].end,newInterval.end);//找到合并后的end值

            i++;

        }

        ret.push_back(tmp);

        while(i<intervals.size()) {//将剩下的Interval都压入ret

            ret.push_back(intervals[i]);

            i++;

        }

        return ret;

    }

};

```