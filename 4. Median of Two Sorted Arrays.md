#<center>一天一道LeetCode<center/>
##（一）题目

> There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

给定两个排好序的数组，求两个数组的中间值。
例如：[1 2]和[1 2] 返回值：1.5

##（二）解题思路
时间复杂度要满足O（log（m+n））， 可以采用一个辅助容器来存储小值，等存到两个数组的一半的时候就停止，再根据奇偶来求中间值。

```
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        vector<int> temp;
        int len1=nums1.size();
        int len2= nums2.size();
        int idx = (len1+len2)/2+1;//需要存放idx个数
        int i =0,j=0;
        int size = 0;
        if(len1 ==0 && len2==0) return 0.0;
        while(size != idx) //当idx==size的时候退出
        {
            if(i == len1 && j<len2)//1遍历完了还没有找到
            {
                temp.push_back(nums2[j]);
                j++;
            }
            else if(i < len1 && j==len2)//2遍历完了还没有找到
            {
                temp.push_back(nums1[i]);
                i++;
            }
            else if(i < len1 && j<len2)//1和2都没有遍历完
            {
                if(nums1[i]<=nums2[j]){
                    temp.push_back(nums1[i]);
                    i++;
                }
                else
                {
                    temp.push_back(nums2[j]);
                    j++;
                }
            }
            size = temp.size();
        }
        if((len1+len2)%2 == 1) return (double)temp[idx-1];
        else return (double)(temp[idx-1]+temp[idx-2])/2;
    }
};
```
该算法遍历（m+n）/2+1次，所以时间复杂度为O（m+n）。
提示：Accepted！

和女票一起做的这题，一开始我用两个指针来求中间值，无奈情况太多考虑不周，代码量太大了，后来才转而用辅助vector。女票半个小时不到就做出来了，用STL的multiset几句代码就搞定的，multiset的insert自带排序，简直逆天！下面贴上她的代码。

```
#include<set>
class Solution {
public:
    double findMedianSortedArrays(int A[], int m, int B[], int n) {
        
        int mid = (m+n+1)/2-1, median1 = 0, median2 = 0;
        multiset<int> mergeArray;
        for(int i = 0; i <　m; i++)
            mergeArray.insert(A[i]);
        for(int i = 0; i < n; i++)
            mergeArray.insert(B[i]);
        
        int i = 0;
        set<int>::iterator iter = mergeArray.begin();
        for(; i++ < mid &&iter != mergeArray.end(); ++iter); 
 
        median1 = *iter;
        iter++;
        median2 = *iter;
       
        if((m+n)%2)
        	return median1;
        else
            return (median1+median2)/2.0;     
    }
};
```

