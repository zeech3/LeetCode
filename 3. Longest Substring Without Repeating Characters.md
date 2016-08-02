#<center>一天一道LeetCode</center>
###（一）题目
> Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without  repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

题目意思：求一字符串中最长的无重复的字符串

###(二) 解题过程
一开始拿到这题，直接暴力解决，用双重循环找无重复的子字符串
结果可想而知，超时！Time Limit Exceeded！

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int max = 0 ;
        for(int i = 0 ; i < s.length();++i)
        {
            int j = i+1;
            int count = 1;
            while(j<s.length())
            {
                int z = j-1;
                while(s[j] != s[z]&&z>=i) z--;//判断是s[j]不等于s[i~j]任一个字符
                if(z+1 == i) count++;//如果不等，则count++
                j++;
            }
            if(max<count) max = count;//记录最大值
        }
        return max;
    }
};
```
O（n^2）的复杂度确实太大了，那么，只能另寻他径了。
降低复杂度的方式：以空间换时间，这里我们可以用到一个数组来记录字符出现过没有。

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int last[256]; //字符的ascII码0~256，记录字符最终出现的位置
        memset(last,-1,sizeof(int)*256);//初始化为-1
        int idx = -1;//用来当前字串开始的位置
        int max = 0;
        for(int i = 0; i < s.length() ; ++i)
        {
            if(last[s[i]]>idx)  //①如果这个字符出现过，则令idx等于上一次出现该字符的位置序号
            {
                idx = last[s[i]];  
            } 
            
            if(i -idx > max){  ②//记录最大的无重复字串
                max = i-idx;
            }
            
            last[s[i]] = i;③
        }
        return max;
    }
};
```
以abca为例：
i=0：查表last['a'] = -1，①不执行 idx=-1， ②执行max =1，更新last表 last['a']  = 0；
i=1：查表last['b'] = -1，①不执行 idx=-1， ②执行max =2，更新last表 last['b']  = 1；
i=2：查表last['c'] = -1，①不执行 idx=-1， ②执行max =3，更新last表 last['c']  = 2；
i=3：查表last['a'] = 0，①执行，idx=0 ， ②执行max =3，更新last表 last['a']  = 3；
.....
上述算法的时间复杂度为O（n），Accepted！