#<center>一天一道LeetCode系列</center>
##（一）题目
>Implement strStr().

>Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

##（二）解题

第一种解法：朴素匹配算法

```cpp

/*

两个指针，分别指向两个字符串的首字符

如果相等则一起向后移动，如果不同i取第一个相同字符的下一个开始继续匹配

如果最后j等于needle的长度则匹配成功，返回i-j

否则返回0

*/

class Solution {

public:

    int strStr(string haystack, string needle) {

        int j,i;

        for(i = 0 , j =0 ; i<haystack.length() && j < needle.length() ;)

        {

            if(i+needle.length()>haystack.length()) return -1;

            if(haystack[i]==needle[j]){//如果匹配上就继续向后匹配

                i++;

                j++;

            }

            else{

                i-=j-1;//回溯到匹配开始时needle的首字符对应的下一位

                j=0;//j回溯到needle的首字符

            }

        }

        if(j==needle.length()) return i-j;

        else return -1;

    }

};

```

第二种解法：KMP模式匹配算法
关于kmp，请自行百度或者大话数据结构P143页

```cpp

class Solution {

public:

    int strStr(string haystack, string needle) {

        int hlen = haystack.length();

        int nlen = needle.length();

        if(hlen==0) return nlen==0?0:-1;//临界值判断

        if(nlen==0) return 0;//needle为NULL，就直接返回0

        int* next = new int[nlen+1];

        getNext(needle,next);

        int i = 0;

        int j = 0;

        while(i<hlen&&j<nlen){

            if(j==-1 || haystack[i]==needle[j]){

                i++;j++;

            }

            else j=next[j];

        }

        if(j==nlen) return i-j;//等于nlen代表匹配成功，返回i-j即needle首字符在haystack中的位置

        else return -1;

    }

    void getNext(string& needle,int next[])

    {

        int i = 0;

        int j = -1;

        next[0] = -1;

        while(i<needle.length()){

            if(j==-1 || needle[i]==needle[j]){

                i++;

                j++;

                if(needle[i] == needle[j]) next[i] = next[j];//kmp优化，防止aaaaab和aaaac前四位的无效                

                else next[i] = j;

            }

            else

                j=next[j];

        }

    }

};

```